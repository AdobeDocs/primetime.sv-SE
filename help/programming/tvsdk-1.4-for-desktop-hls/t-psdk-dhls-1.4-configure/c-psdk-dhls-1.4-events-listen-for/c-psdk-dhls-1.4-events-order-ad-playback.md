---
description: När din uppspelning inkluderar annonsering skickar TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.
title: Ordning på annonsevenemang
exl-id: 131b1dc1-3a59-4276-b639-d004ab7394ea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Ordning på annonsevenemang{#order-of-advertising-events}

När din uppspelning inkluderar annonsering skickar TVSDK händelser/meddelanden i de sekvenser som förväntas. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

När annonser spelas upp är händelseordningen:

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* Följande skickas för varje annons i annonsbrytningen:

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (flera gånger under en annons uppspelning)
   * `AdClickEvent.AD_CLICK` (för varje klick)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

I följande exempel visas ett typiskt förlopp för annonsuppspelningshändelser:

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```
