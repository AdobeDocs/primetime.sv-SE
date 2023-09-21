---
description: Du kan konfigurera visuellt för att meddela användaren att innehållet buffras.
title: Buffring
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Buffring{#buffering}

Du kan konfigurera visuellt för att meddela användaren att innehållet buffras.

Lyssna efter `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` och `AdobePSDK.PSDKEventType.BUFFERING_END` händelser. Till exempel:

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

UI Framework innehåller standardimplementering av buffringsövertäckning, som kan utökas enligt nedan:

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

Så här ser resultatet DOM ut:

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```
