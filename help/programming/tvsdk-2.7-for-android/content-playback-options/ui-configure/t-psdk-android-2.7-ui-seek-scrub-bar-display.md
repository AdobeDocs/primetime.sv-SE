---
description: TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i VOD (video on demand) och liveströmmar.
title: Visa ett söknavigeringsfält med den aktuella uppspelningspositionen
exl-id: fb1a87ec-30ab-4dbe-9744-720eac523542
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Visa ett söknavigeringsfält med den aktuella uppspelningspositionen {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i VOD (video on demand) och liveströmmar.

>[!TIP]
>
>Sökning i en liveström är endast tillåtet för DVR.

1. Konfigurera återanrop för sökning.

       Sökningen är asynkron, så TVSDK skickar följande sökrelaterade händelser:
   
   * `MediaPlayerEvent.SEEK_BEGIN`, där sökningen börjar.
   * `MediaPlayerEvent.SEEK_END`, där sökningen lyckas.
   * `MediaPlayerEvent.OPERATION_FAILED`, där sökningen har misslyckats.

1. Vänta tills spelaren har en giltig status för sökning.

   Giltiga statusvärden är PREPARED, COMPLETE, PAUSED och PLAYING.
1. Använd det inbyggda `SeekBar` att ange `OnSeekBarChangeListener`, som avgör när användaren stegar igenom.
1. Skicka den begärda sökpositionen (millisekunder) till `MediaPlayer.seek` -metod.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Du kan bara söka efter resursens sökbara längd. För video on demand är det från 0 till resursens längd.

   >[!TIP]
   >
   >Det här steget flyttar spelhuvudet till en ny position i strömmen, men den slutliga beräknade positionen kan skilja sig från den angivna sökpositionen.

1. Lyssna efter `MediaPlayerEvent.OPERATION_FAILED` och vidta lämpliga åtgärder.

   Den här händelsen skickar lämplig varning. Programmet avgör hur du ska gå vidare, och alternativen omfattar att försöka söka igen eller fortsätta uppspelningen från den föregående positionen.

1. Vänta på att TVSDK ska ringa `MediaPlayerEvent.SEEK_END` återanrop.
1. Hämta den slutliga justerade uppspelningspositionen med återanropets positionsparameter.

   Detta är viktigt eftersom den faktiska startpositionen efter sökningen kan skilja sig från den begärda positionen. Regler, inklusive uppspelningsbeteendet påverkas om en sökning eller annan omplacering avslutas mitt i en annonsbrytning eller hoppar över och brytningar kan tillämpas.

1. Använd positionsinformationen när du visar en sökningslist.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Söker efter exempel**

I det här exemplet drar användaren sökfältet för att söka till önskad position.

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()), 
        playbackRange.getDuration()); 
     
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```
