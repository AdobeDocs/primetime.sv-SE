---
description: Registrera lämpliga händelseavlyssnare om du vill få meddelanden om tidslinjeuppdateringar.
seo-description: Registrera lämpliga händelseavlyssnare om du vill få meddelanden om tidslinjeuppdateringar.
seo-title: Lägga till avlyssnare för TimelineUpdatedEvent
title: Lägga till avlyssnare för TimelineUpdatedEvent
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Lägga till avlyssnare för TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Registrera lämpliga händelseavlyssnare om du vill få meddelanden om tidslinjeuppdateringar.

Varje gång tidslinjen uppdateras skickas `MediaPlayer` texten `AdobePSDK.TimelineEvent` med text `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implementera lämpliga avlyssnare.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. Registrera händelseavlyssnarna.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

