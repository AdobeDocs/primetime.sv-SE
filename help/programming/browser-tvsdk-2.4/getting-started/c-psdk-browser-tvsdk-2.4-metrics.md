---
description: Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.
title: Mått
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# Mått{#metrics}

Webbläsarens TVSDK innehåller mätvärden som kan användas för analys och felsökning. Du kan hämta dessa mått med QoSProvider.

Exempel:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

