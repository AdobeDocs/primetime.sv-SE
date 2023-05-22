---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. Webbläsarens TVSDK innehåller detaljerad statistik om uppspelning, buffring och enheter.
title: Kvalitetsstatistik för tjänster
exl-id: b7486ed5-e59f-428c-942c-a2fee7a869c9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Kvalitetsstatistik för tjänster{#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. Webbläsarens TVSDK innehåller detaljerad statistik om uppspelning, buffring och enheter.

## Läs QOS-uppspelning, buffring och enhetsstatistik {#read-qos-playback-buffering-and-device-statistics}

Du kan läsa uppspelning, buffring och enhetsstatistik från klassen QOSProvider.

The `QOSProvider` -klassen innehåller olika statistik, bland annat information om buffring, bithastigheter, bildrutehastigheter och tidsdata.

1. Skapa en mediespelare.
1. Skapa en `QOSProvider` och bifoga det till mediespelaren.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Valfritt) Läs uppspelningsstatistiken.

   En lösning för att läsa uppspelningsstatistik är att ha en timer som regelbundet hämtar de nya QoS-värdena från `QOSProvider`. Till exempel:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. (Valfritt) Läs enhetsspecifik information.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
