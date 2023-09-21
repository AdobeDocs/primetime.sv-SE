---
description: Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.
title: Visa videons varaktighet, aktuella tid och återstående tid
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Visa videons varaktighet, aktuella tid och återstående tid{#display-the-duration-current-time-and-remaining-time-of-the-video}

Du kan använda TVSDK för att hämta information om media som du kan visa i sökfältet.

1. Vänta tills spelaren är i tillståndet PREPARED.
1. Hämta den aktuella spelhuvudstiden med `MediaPlayer.getCurrentTime` -metod.

   Detta returnerar spelhuvudets aktuella position på den virtuella tidslinjen i millisekunder. Tiden beräknas i förhållande till den matchade strömmen som kan innehålla flera instanser av alternativt innehåll, till exempel flera annonser eller annonsbrytningar som delas upp i huvudströmmen. För live-/linjära strömmar är den returnerade tiden alltid i uppspelningsfönsterintervallet.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Hämta uppspelningsintervallet för strömmen och fastställ varaktigheten.
   1. Använd `mediaPlayer.getPlaybackRange` metod för att hämta tidsintervallet för den virtuella tidslinjen.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Tolka tidsintervallet med `mediacore.utils.TimeRange`.
   1. Ta bort början från intervallets slut om du vill bestämma varaktigheten.

      Detta omfattar längden på ytterligare innehåll som infogas i strömmen (annonser).

      För VOD börjar intervallet alltid med noll och slutvärdet är lika med summan av innehållets längd och varaktigheten för ytterligare innehåll som infogas i flödet (annonser).

      För en linjär/liveresurs representerar intervallet uppspelningsfönstret och det här intervallet ändras under uppspelningen.

      TVSDK ringer din `onUpdated` återanrop som anger att medieobjektet uppdaterades och att dess attribut (inklusive uppspelningsintervallet) uppdaterades.

1. Använd de metoder som finns på `MediaPlayer` och `SeekBar` klass som är allmänt tillgänglig i Android SDK för att ställa in sökfältsparametrarna.

   Här är till exempel en möjlig layout som innehåller `SeekBar` och två `TextView` -element.

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

   I följande exempel används `Clock.java` hjälpklass som timer, som är tillgänglig i referensspelaren PrimetimeReference. Den här klassen ställer in en händelseavlyssnare och utlöser en `onTick` -händelse varje sekund eller ett annat timeout-värde som du kan ange.

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
