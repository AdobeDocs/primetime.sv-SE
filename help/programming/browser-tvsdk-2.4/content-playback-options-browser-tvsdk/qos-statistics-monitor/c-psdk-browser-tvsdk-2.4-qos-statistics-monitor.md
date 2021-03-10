---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. Webbläsarens TVSDK innehåller detaljerad statistik om uppspelning, buffring och enheter.
title: Kvalitetsstatistik för tjänster
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# Kvalitetsstatistik för tjänster{#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. Webbläsarens TVSDK innehåller detaljerad statistik om uppspelning, buffring och enheter.

## Läs QOS-uppspelning, buffring och enhetsstatistik {#read-qos-playback-buffering-and-device-statistics}

Du kan läsa uppspelning, buffring och enhetsstatistik från klassen QOSProvider.

Klassen `QOSProvider` innehåller olika statistik, bland annat information om buffring, bithastigheter, bildrutefrekvenser och tidsdata.

1. Skapa en mediespelare.
1. Skapa ett `QOSProvider`-objekt och koppla det till mediespelaren.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Valfritt) Läs uppspelningsstatistiken.

   En lösning för att läsa uppspelningsstatistik är att ha en timer som regelbundet hämtar de nya QoS-värdena från `QOSProvider`. Exempel:

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
