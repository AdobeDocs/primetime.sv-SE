---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
title: Kvalitetsstatistik för tjänster
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Kvalitetsstatistik för tjänsten {#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.

## Läs QOS-uppspelning, buffring och enhetsstatistik {#section_9996406E2D814FA382B77E3041CB02BC}

Du kan läsa uppspelning, buffring och enhetsstatistik från klassen `PTQOSProvider`.

Klassen `PTQOSProvider` innehåller olika statistik, bland annat information om buffring, bithastigheter, bildrutefrekvenser och tidsdata.

Det innehåller även information om enheten, till exempel modell, operativsystem och tillverkarens enhets-ID.

>[!TIP]
>
>Du kan inte ändra storleken på uppspelningsbufferten, men du kan övervaka statusen för buffertstorleken för felsökning eller analys. `PTPlaybackInformation` innehåller egenskaper som  `playbackBufferFull` och  `playbackLikelyToKeepUp`.

1. Skapa en mediespelare.
1. Skapa ett `PTQOSProvider`-objekt och koppla det till mediespelaren.

   Konstruktorn `PTQOSProvider` har en spelarkontext så att den kan hämta enhetsspecifik information.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Valfritt) Läs uppspelningsstatistiken.

   En lösning för att läsa uppspelningsstatistik är att ha en timer, t.ex. en `NSTimer`, som regelbundet hämtar de nya QoS-värdena från `PTQOSProvider`. Exempel:

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. (Valfritt) Läs enhetsspecifik information.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
