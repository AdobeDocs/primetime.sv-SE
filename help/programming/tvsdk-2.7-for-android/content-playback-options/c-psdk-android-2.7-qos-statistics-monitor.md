---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
seo-description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
seo-title: Kvalitetsstatistik för tjänster
title: Kvalitetsstatistik för tjänster
uuid: 8e990461-065b-4efa-b77c-b2b832f86f7d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Kvalitetsstatistik för tjänsten {#quality-of-service-statistics}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.

TVSDK tillhandahåller även information om följande hämtade resurser:

* Spellistor/manifestfiler
* Filfragment
* Spåra information om filer

## Spåra på fragmentnivå med hjälp av inläsningsinformation {#section_4439D91E8EDC45588EF1D7BE25697350}

Du kan läsa QoS-information (Quality of Service) om hämtade resurser, som fragment och spår, från klassen `LoadInformation`.

1. Implementera och registrera händelseavlyssnaren `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`.
1. Anropa `event.getLoadInformation()` för att läsa relevanta data från parametern `event` som skickas till återanropet.

   >[!NOTE]
   >
   >Mer information om `LoadInformation` finns i [2.7 för Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API-dokument.

## Läs QOS-uppspelning, buffring och enhetsstatistik {#section_D21722600F324E67A9F06234D338B243}

Du kan läsa uppspelning, buffring och enhetsstatistik från klassen `QOSProvider`.

Klassen `QOSProvider` innehåller olika statistik, bland annat information om buffring, bithastigheter, bildrutefrekvenser och tidsdata. Den innehåller även information om enheten, t.ex. tillverkare, modell, operativsystem, SDK-version, tillverkarens enhets-ID och skärmstorlek/skärmtäthet.

1. Skapa en mediespelare.
1. Skapa ett `QOSProvider`-objekt och koppla det till mediespelaren.

   Konstruktorn `QOSProvider` har en spelarkontext så att den kan hämta enhetsspecifik information.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Valfritt) Läs uppspelningsstatistiken.

   En lösning för att läsa uppspelningsstatistik är att ha en timer som regelbundet hämtar de nya QoS-värdena från `QOSProvider`.

   Exempel:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. (Valfritt) Läs enhetsspecifik information.

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```

