---
description: TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.
title: Ordning för uppspelningshändelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Ordning för uppspelningshändelser{#order-of-playback-events}

TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

I följande exempel visas ordningen för vissa händelser som innehåller uppspelningshändelser.

* När en medieresurs läses in `MediaPlayer.replaceCurrentResource`, är händelseordningen:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` med status `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` med status `MediaPlayerStatus.INITIALIZED`

* När du förbereder för uppspelning genom `MediaPlayer.prepareToPlay`, är händelseordningen:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` med status `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` om annonser har infogats
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` med status `MediaPlayerStatus.PREPARED`

* För live-/linjära strömmar, under uppspelningen när uppspelningsfönstret går framåt och ytterligare möjligheter är lösta, är händelseordningen:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` om annonser har infogats

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

I följande exempel visas ett typiskt händelseförlopp:

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```
