---
description: I det här exemplet visas det rekommenderade sättet att inkludera anpassade annonsmarkörer på tidslinjen för uppspelningen.
title: Placera anpassade annonsmarkörer på tidslinjen
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Placera anpassade annonsmarkörer på tidslinjen {#place-custom-ad-markers-on-the-timeline}

I det här exemplet visas det rekommenderade sättet att inkludera anpassade annonsmarkörer på tidslinjen för uppspelningen.

1. Översätt informationen om annonsplacering utanför band till en lista/array med `RepaceTimeRange` klassen.
1. Skapa en instans av `CustomRangeMetadata` och använda dess `setTimeRangeList` metoden med list/array som argument för att ange sin lista över tidsintervall.
1. Använd `setType` metod för att ställa in typen på `MARK_RANGE`.
1. Använd `MediaPlayerItemConfig.setCustomRangeMetadata` metoden med `CustomRangeMetadata` -instans som argument för att ange metadata för det anpassade intervallet.
1. Använd `MediaPlayer.replaceCurrentResource` metoden med `MediaPlayerItemConfig` -instans som argument för att ange att den nya resursen ska vara den aktuella.
1. Vänta på en `STATE_CHANGED` -händelse, som rapporterar att spelaren finns i `PREPARED` tillstånd.
1. Starta videouppspelning genom att anropa `MediaPlayer.play`.

Här är resultatet av att du har slutfört uppgifterna i det här exemplet:

* Om en `ReplaceTimeRange` överlappar varandra på uppspelningstidslinjen, t.ex. startpositionen för en `ReplaceTimeRange` är tidigare än en redan placerad slutposition, justerar TVSDK i tysthet början på den felaktiga `ReplaceTimeRange` för att undvika konflikten.

  Detta gör att de justerade `ReplaceTimeRange` kortare än ursprungligen angivet. Om justeringen leder till en varaktighet på noll, släpper TVSDK tyst det felaktiga `ReplaceTimeRange`.

* TVSDK söker efter närliggande tidsintervall för anpassade annonsbrytningar och grupperar dem i separata annonsbrytningar.

Tidsintervall som inte ligger intill något annat tidsintervall översätts till annonsbrytningar som innehåller en enda annons.

* Om programmet försöker läsa in en medieresurs vars konfiguration innehåller `CustomRangeMetadata` som bara kan användas i anpassade annonseringsmarkörer, genererar TVSDK ett undantag om den underliggande tillgången inte är av typen VOD.

* När TVSDK hanterar anpassade annonsmarkörer inaktiveras andra annonslösningsmekanismer (till exempel Adobe Primetime annonsbeslut).

  Du kan använda valfri annonsmodul för TVSDK eller en anpassad annonsmarkörmekanism. När du använder anpassade annonsmarkörer tolkas annonsinnehållet som löst och placeras på tidslinjen.

Följande kodfragment placerar tre tidsintervall på tidslinjen som anpassade annonsmarkörer.

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
