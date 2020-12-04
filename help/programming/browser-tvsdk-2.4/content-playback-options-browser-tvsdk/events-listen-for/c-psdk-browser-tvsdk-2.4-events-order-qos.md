---
description: Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.
seo-description: Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.
seo-title: QoS-händelser
title: QoS-händelser
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# QoS-händelser{#qos-events}

Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.

Om du vill få meddelanden om alla QoS-relaterade händelser skapar du en instans av `AdobePSDK.QOSProvider` och kopplar MediaPlayer-instansen till den här `QOSProvider`-instansen:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Konfigurera en timer i programmet för att regelbundet kontrollera egenskapen `playbackInformation` för instansen `qosProvider`. Egenskapen `playbackInformation` ger en ögonblicksbild av aktuell uppspelningsstatistik. Exempel:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

