---
description: Här är några exempel på processen att ta bort och ersätta annonser.
seo-description: Här är några exempel på processen att ta bort och ersätta annonser.
seo-title: Exempel på att ta bort och ersätta annonser
title: Exempel på att ta bort och ersätta annonser
uuid: 31ceb39a-aa30-472e-908a-3ba57559045f
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Exempel på att ta bort och ersätta annonser {#examples-to-delete-and-replace-ads}

Här är några exempel på processen att ta bort och ersätta annonser.

Här är ett exempel på hur du använder `DELETE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means,  
// like a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, o)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.DELETE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource  
mediaPlayer.replaceCurrentResource(mediaResource, config);
```

Här är ett exempel på hur du använder `REPLACE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means, like 
//  a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 10000)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 20000)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 30000)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.REPLACE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config = new MediaPlayerItemConfig(getActivity() 
    .getApplicationContext()); 
 
// Set Auditude settings, which are used for ad replacement, for this  
//  MediaPlayerItemConfig instance, 
 
... 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource 
mediaPlayer.replaceCurrentResource(mediaResource, config);
```

