---
description: Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.
title: Mått
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Mått{#metrics}

Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.

Till exempel:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
