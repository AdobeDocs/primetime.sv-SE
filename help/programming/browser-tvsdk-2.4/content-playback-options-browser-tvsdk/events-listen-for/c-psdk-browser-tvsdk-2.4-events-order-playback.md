---
description: Webbläsarens TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.
title: Ordning för uppspelningshändelser
exl-id: fd9dc0d5-0f39-4a6d-9d88-1fd49946fedf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Ordning för uppspelningshändelser{#order-of-playback-events}

Webbläsarens TVSDK skickar händelser/meddelanden i vanligtvis förväntade sekvenser. Spelaren kan implementera åtgärder baserat på händelser i den förväntade sekvensen.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

I följande exempel visas ordningen för vissa händelser som innehåller uppspelningshändelser.

* När en medieresurs läses in `replaceCurrentResource`, är händelseordningen:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* När du förbereder för uppspelning genom `MediaPlayer.prepareToPlay`, är händelseordningen:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

I följande exempel visas ett typiskt händelseförlopp:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```
