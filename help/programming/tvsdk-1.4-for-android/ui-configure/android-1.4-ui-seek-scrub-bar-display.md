---
description: TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i både VOD (video on demand) och liveströmmar.
title: Visa ett söknavigeringsfält med aktuell uppspelningsposition
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Visa ett söknavigeringsfält med aktuell uppspelningsposition {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK har stöd för sökning till en viss position (tid) där strömmen är en spelningslista med skjutbara fönster, i både VOD (video on demand) och liveströmmar.

>[!IMPORTANT]
>
>Sökning i en liveström är endast tillåtet för DVR.

1. Konfigurera återanrop för sökning.

       Sökningen är asynkron, så TVSDK skickar följande sökrelaterade händelser:
   
   * `QOSEventListener.onSeekStart` - Sök efter start.
   * `QOSEventListener.onSeekComplete` - Sökningen lyckades.
   * `QOSEventListener.onOperationFailed` - Sökningen misslyckades.

1. Vänta tills spelaren är i ett giltigt söktillstånd.

   Giltiga lägen är PREPARED, COMPLETE, PAUSED och PLAYING.

1. Använd den inbyggda SeekBar för att ange `OnSeekBarChangeListener` för att se när användaren drar.
1. Lyssna efter `QOSEventListener.onOperationFailed` och vidta lämpliga åtgärder.

   Den här händelsen skickar lämplig varning. Programmet avgör till exempel hur du ska gå vidare genom att försöka söka igen eller fortsätta uppspelningen från föregående position.

1. Vänta på att TVSDK ska ringa `QOSEventListener.onSeekComplete` återanrop.
1. Hämta den slutliga justerade uppspelningspositionen med återanropets positionsparameter.

   Detta är viktigt eftersom den faktiska startpositionen efter sökningen kan skilja sig från den begärda positionen. Uppspelningsbeteendet kan påverkas om en sökning eller annan omplacering slutar mitt i en annonsbrytning eller hoppar över annonsbrytningar.

1. Använd positionsinformationen när du visar en sökningslist.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Söker efter exempel**

I det här exemplet drar användaren sökfältet för att söka till önskad position.

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
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
