---
description: Registrera lämpliga händelseavlyssnare om du vill få meddelanden om tidslinjeuppdateringar.
title: Lägga till avlyssnare för TimelineUpdatedEvent
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Lägga till avlyssnare för TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Registrera lämpliga händelseavlyssnare om du vill få meddelanden om tidslinjeuppdateringar.

Varje gång tidslinjen uppdateras visas `MediaPlayer` utskick `AdobePSDK.TimelineEvent` med text `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
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
