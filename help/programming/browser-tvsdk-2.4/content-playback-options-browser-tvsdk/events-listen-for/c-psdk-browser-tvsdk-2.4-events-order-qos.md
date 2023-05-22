---
description: Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.
title: QoS-händelser
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# QoS-händelser{#qos-events}

Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.

Om du vill få meddelanden om alla QoS-relaterade händelser skapar du en instans av `AdobePSDK.QOSProvider` och bifoga MediaPlayer-instansen till detta `QOSProvider` instans:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Konfigurera en timer i programmet för att regelbundet kontrollera `playbackInformation` egenskapen för `qosProvider` -instans. The `playbackInformation` -egenskapen ger en ögonblicksbild av aktuell uppspelningsstatistik. Till exempel:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
