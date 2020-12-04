---
description: Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.
seo-description: Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.
seo-title: Mått
title: Mått
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---


# Mått{#metrics}

Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.

Exempel:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

