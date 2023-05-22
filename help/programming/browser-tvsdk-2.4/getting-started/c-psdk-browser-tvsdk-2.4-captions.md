---
description: Du kan visa beskrivningar när du spelar upp videoinnehåll.
title: Bildtexter
exl-id: 2144a6b2-0b9a-49ea-ad44-997adf36cbe6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Bildtexter{#captions}

Du kan visa beskrivningar när du spelar upp videoinnehåll.

Om du vill hantera bildtexter måste du lägga till `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` händelseavlyssnare:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<pre>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</pre>
```

UI Framework innehåller en standardimplementering av bildtexter som kan ändras. Du kan också ändra beteenden för undertexter genom att utöka standardbeteenden för undertexter. Till exempel:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer(‘.videoDiv', { 
player:{ 
    mediaResource: 'Specify Resource URL', 
    ccStyle: { 
    font:AdobePSDK.TextFormat.CURSIVE, 
    fontColor:AdobePSDK.TextFormat.BRIGHT_WHITE, 
    edgeColor:AdobePSDK.TextFormat.BLUE, 
    backgroundColor:AdobePSDK.TextFormat.BLACK, 
    fillColor:AdobePSDK.TextFormat.BLUE, 
    size:AdobePSDK.TextFormat.MEDIUM, 
    fontOpacity:100, 
    backgroundOpacity:1, 
    fillOpacity:1 
   } 
 } 
 
}); 
```
