---
description: Du kan använda TVSDK för att hämta information om spelarens position i mediet och visa den i sökfältet.
title: Visa videons varaktighet, aktuella tid och återstående tid
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Visa videons varaktighet, aktuella tid och återstående tid {#display-the-duration-current-time-and-remaining-time-of-the-video}

Du kan använda TVSDK för att hämta information om spelarens position i mediet och visa den i sökfältet.

1. Vänta tills spelaren är i åtminstone tillståndet PREPARED.
1. Hämta aktuell spelhuvudtid med metoden `MediaPlayer.getCurrentTime`.

   Detta returnerar spelhuvudets aktuella position på den virtuella tidslinjen i millisekunder. Tiden beräknas i förhållande till den matchade strömmen som kan innehålla flera instanser av alternativt innehåll, till exempel flera annonser eller annonsbrytningar som delas upp i huvudströmmen. För live-/linjära strömmar är den returnerade tiden alltid i uppspelningsfönsterintervallet.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Hämta uppspelningsintervallet för strömmen och fastställ varaktigheten.
   1. Använd metoden `MediaPlayer.getPlaybackRange` för att hämta tidsintervallet för den virtuella tidslinjen.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Använd metoden `MediaPlayer.getPlaybackRange` för att hämta tidsintervallet för den virtuella tidslinjen.

      * För VOD börjar intervallet alltid med noll och slutvärdet är lika med summan av innehållets längd och varaktigheten för ytterligare innehåll i flödet (annonser).
      * För en linjär/liveresurs representerar intervallet uppspelningsfönsterintervallet. Det här intervallet ändras under uppspelning.

         TVSDK anropar återanropet `ITEM_Updated` för att ange att medieobjektet uppdaterades och att dess attribut, inklusive uppspelningsintervallet, uppdaterades.

1. Använd de metoder som är tillgängliga i `MediaPlayer` och i klassen `SeekBar` i Android SDK för att ställa in sökfältsparametrarna.

   Här finns till exempel en möjlig layout som innehåller sökfältet och två `TextView`-element.

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

1. Använd en timer för att regelbundet hämta den aktuella tiden och uppdatera sökfältet enligt bilden:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   I följande exempel används hjälpklassen `Clock.java`, som är tillgänglig i `ReferencePlayer`, som timer. Den här klassen ställer in en händelseavlyssnare och utlöser en `onTick`-händelse varje sekund, eller ett annat timeout-värde som du kan ange.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   I det här exemplet hämtas mediespelarens aktuella position och sökfältet uppdateras. De två `TextView`-elementen används för att markera den aktuella tiden och slutpositionen för uppspelningsintervallet som numeriska värden.

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
