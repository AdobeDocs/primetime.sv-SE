---
description: Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.
title: QoS-händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
