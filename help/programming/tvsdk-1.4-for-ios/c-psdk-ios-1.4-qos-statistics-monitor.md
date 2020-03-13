---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
seo-description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
seo-title: Kvalitetsstatistik för tjänster
title: Kvalitetsstatistik för tjänster
uuid: b74cbc94-1d69-4b4b-b969-d0e985b4762b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Kvalitetsstatistik för tjänster{#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.

## Läs QOS-uppspelning, buffring och enhetsstatistik {#section_9996406E2D814FA382B77E3041CB02BC}

Du kan läsa uppspelning, buffring och enhetsstatistik från `PTQOSProvider` klassen.

Klassen innehåller `PTQOSProvider` olika statistik, bland annat information om buffring, bithastigheter, bildrutehastigheter och tidsdata.

Det innehåller även information om enheten, till exempel modell, operativsystem och tillverkarens enhets-ID.

>[!TIP]
>
>Du kan inte ändra storleken på uppspelningsbufferten, men du kan övervaka statusen för buffertstorleken för felsökning eller analys. `PTPlaybackInformation` innehåller egenskaper som `playbackBufferFull` och `playbackLikelyToKeepUp`.

1. Skapa en mediespelare.
1. Skapa ett `PTQOSProvider` objekt och bifoga det till mediespelaren.

   Konstruktorn använder en spelarkontext så att den kan hämta enhetsspecifik information. `PTQOSProvider`

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

