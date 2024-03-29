---
description: Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.
title: Spara videopositionen och återuppta den senare
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Spara videopositionen och återuppta den senare {#save-the-video-position-and-resume-later}

Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.

Annonser som infogats dynamiskt skiljer sig mellan användarsessioner, så att positionen sparas **med** delade annonser avser en annan position i en framtida session. TVSDK innehåller metoder för att hämta uppspelningspositionen samtidigt som delade annonser ignoreras.

1. När användaren avslutar en video hämtas och sparas positionen i videon.

   >[!TIP]
   >
   >Annonslängder ingår inte.

   Annonsbrytningar kan variera mellan olika sessioner på grund av annonsmönster, frekvensbegränsning och så vidare. Den aktuella tidpunkten för videon i en session kan vara annorlunda i en framtida session. När du sparar en position i videon hämtar programmet lokal tid, som du kan spara på enheten eller i en databas på servern.

   Om användaren till exempel är på den 20:e minuten av videon och den här positionen innehåller fem minuters annonser, `getCurrentTime` kommer att returnera 1200 sekunder, medan `getLocalTime` vid denna position kommer att returnera 900 sekunder.

   >[!IMPORTANT]
   >
   >Lokal tid och aktuell tid är samma för live/linjära strömmar. I detta fall `convertToLocalTime` har ingen effekt. För VOD ändras inte lokal tid medan annonser spelas upp.

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. Återställ användarsessionen när spelaraktiviteten återupptas.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. Så här återupptar du videon på samma plats:

   * Om du vill återuppta uppspelningen av videon från den position som sparades från en tidigare session använder du `seekToLocalTime`.

     >[!TIP]
     >
     >Den här metoden anropas bara med lokala tidsvärden. Om metoden anropas med aktuella tidsresultat inträffar ett felaktigt beteende.

   * Om du vill söka till aktuell tid använder du `seek`.

1. När ditt program får `onStatusChanged` statusändringshändelse, söka till den sparade lokala tiden.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. Ange annonsbrytningarna som de anges i annonsprincipgränssnittet.
1. Implementera en anpassad annonsprincipväljare genom att utöka standardväljaren för annonsprinciper.
1. Ange de annonsbrytningar som måste presenteras för användaren genom att implementera `selectAdBreaksToPlay`.

   Den här metoden innehåller en annonsbrytning före rullning och annonsen i mitten av rullen bryts före den lokala tidspositionen. Ditt program kan bestämma sig för att spela upp en annonsbrytning i förväg och återuppta den angivna lokala tiden, spela upp en annonsbrytning i mellanrummet och återuppta den angivna lokala tiden eller spela upp inga annonsbrytningar.
