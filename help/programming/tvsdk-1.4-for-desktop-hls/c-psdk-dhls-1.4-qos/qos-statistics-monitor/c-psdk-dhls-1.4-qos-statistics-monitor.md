---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
title: Kvalitetsstatistik för tjänster
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Kvalitetsstatistik för tjänsten {#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.

TVSDK tillhandahåller även information om följande hämtade resurser:

* Spellistor/manifestfiler
* Filfragment
* Spåra information om filer

## Spåra på fragmentnivå med hjälp av inläsningsinformation {#track-at-the-fragment-level-using-load-information}

Du kan läsa QoS-information (Quality of Service) om hämtade resurser, som fragment och spår, från klassen LoadInformation.

1. Implementera händelseavlyssnaren `onLoadInformationAvailable` för återanrop.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registrera händelseavlyssnaren, som TVSDK anropar varje gång ett fragment har hämtats.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Läs intressanta data från `LoadInformation` som skickas till återanropet.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Egenskap </th> 
      <th colname="col1" class="entry"> Typ </th> 
      <th colname="col2" class="entry"> Beskrivning </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <p>Nummer </p> </td> 
      <td colname="col2"> <p>Hämtningens varaktighet i millisekunder. </p> <p>TVSDK skiljer inte mellan den tid det tog för klienten att ansluta till servern och den tid det tog att hämta det fullständiga fragmentet. Om till exempel ett 10 MB-segment tar 8 sekunder att ladda ned, tillhandahåller TVSDK den informationen, men talar inte om för dig att det tog 4 sekunder innan den första byten och ytterligare 4 sekunder att ladda ned hela fragmentet. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>Nummer </p> </td> 
      <td colname="col2"> Medielängden för de hämtade fragmenten i millisekunder. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <p>Nummer </p> </td> 
      <td colname="col2"> Storleken på den hämtade resursen i byte. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> Index för motsvarande spår, om det är känt. annars 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>Sträng </p> </td> 
      <td colname="col2"> Namnet på motsvarande spår, om det är känt. annars null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>Sträng </p> </td> 
      <td colname="col2"> Typ av motsvarande spår, om den är känd. annars null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <p>Sträng </p> </td> 
      <td colname="col2"> Vad TVSDK laddade ned. Något av följande: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - En spellista/ett manifest </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENT - Ett fragment </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - Ett fragment som är associerat med ett visst spår </li> 
      </ul> Ibland är det inte möjligt att identifiera resurstypen. Om detta inträffar returneras FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>Sträng </p> </td> 
      <td colname="col2"> Den URL som pekar på den hämtade resursen. </td> 
   </tr> 
   </tbody> 
   </table>

## Läs QOS-uppspelning, buffring och enhetsstatistik {#read-qos-playback-buffering-and-device-statistics}

Du kan läsa uppspelning, buffring och enhetsstatistik från klassen QOSProvider.

Klassen `QOSProvider` innehåller olika statistik, bland annat information om buffring, bithastigheter, bildrutefrekvenser och tidsdata.

Det innehåller även information om enheten, t.ex. tillverkare, modell, operativsystem, SDK-version och skärmstorlek/skärmtäthet.

1. Skapa en mediespelare.
1. Skapa ett `QOSProvider`-objekt och koppla det till mediespelaren.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Valfritt) Läs uppspelningsstatistiken.

   En lösning för att läsa uppspelningsstatistik är att ha en timer som regelbundet hämtar de nya QoS-värdena från `QOSProvider`. Exempel:

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (Valfritt) Läs enhetsspecifik information.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```
