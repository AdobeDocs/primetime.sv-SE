---
description: Browser TVSDK skickar QoS-händelser (Quality of Service) för att meddela programmet om händelser som kan påverka beräkningen av QoS-statistik, som buffring och sökning av händelser.
title: QoS-händelser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
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

