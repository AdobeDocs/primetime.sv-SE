---
description: Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.
seo-description: Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.
seo-title: Visa videons varaktighet, aktuella tid och återstående tid
title: Visa videons varaktighet, aktuella tid och återstående tid
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Visa videons varaktighet, aktuella tid och återstående tid{#display-the-duration-current-time-and-remaining-time-of-the-video}

Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.

1. Vänta tills spelaren är i tillståndet PREPARED.
1. Hämta den aktuella spelhuvudstiden med metoden `MediaPlayer.getCurrentTime`.

   Detta returnerar spelhuvudets aktuella position på den virtuella tidslinjen i millisekunder. Tiden beräknas i förhållande till den matchade strömmen som kan innehålla flera instanser av alternativt innehåll, till exempel flera annonser eller annonsbrytningar som delas upp i huvudströmmen. För live-/linjära strömmar är den returnerade tiden alltid i uppspelningsfönsterintervallet.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Hämta uppspelningsintervallet för strömmen och fastställ varaktigheten.
   1. Använd metoden `mediaPlayer.getPlaybackRange` för att hämta tidsintervallet för den virtuella tidslinjen.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Tolka tidsintervallet med `mediacore.utils.TimeRange`.
   1. Ta bort början från intervallets slut om du vill bestämma varaktigheten.

      Detta omfattar längden på ytterligare innehåll som infogas i strömmen (annonser).

      För VOD börjar intervallet alltid med noll och slutvärdet är lika med summan av innehållets längd och varaktigheten för ytterligare innehåll som infogas i flödet (annonser).

      För en linjär/liveresurs representerar intervallet uppspelningsfönstret och det här intervallet ändras under uppspelningen.

      TVSDK anropar ditt `onUpdated`-återanrop för att ange att medieobjektet har uppdaterats och att dess attribut (inklusive uppspelningsintervallet) har uppdaterats.

1. Använd de metoder som är tillgängliga för klassen `MediaPlayer` och klassen `SeekBar` som är allmänt tillgänglig i Android SDK för att ställa in sökfältsparametrarna.

   Det finns till exempel en möjlig layout som innehåller `SeekBar` och två `TextView`-element.

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. Använd en timer för att regelbundet hämta aktuell tid och uppdatera SeekBar.

   I följande exempel används hjälpklassen `Clock.java` som timer, som är tillgänglig i referensspelaren PrimetimeReference. Den här klassen ställer in en händelseavlyssnare och utlöser en `onTick`-händelse varje sekund, eller ett annat timeout-värde som du kan ange.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   Vid varje klockslag hämtar det här exemplet mediespelarens aktuella position och uppdaterar SeekBar. De två TextView-elementen används för att markera den aktuella tiden och uppspelningsintervallets slutposition som numeriska värden.

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```

