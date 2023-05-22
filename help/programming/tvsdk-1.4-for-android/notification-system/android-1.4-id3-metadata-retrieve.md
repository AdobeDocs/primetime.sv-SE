---
description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
title: ID3-taggar
exl-id: a0b6ef0b-a8e1-44fa-ab34-3be60a2997c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# ID3-taggar {#id-tags}

ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.

>[!IMPORTANT]
>
>TVSDK känner igen ID3-metadata (version 2.3.0 eller 2.4.0) i ljud- (AAC) och videoströmmar (H.264) i någon av dess möjliga kodningar (ASCII, UTF8, UTF16-BE eller UTF16-LE). Den ignorerar ID3-taggar som inte finns i någon av de godkända versionerna eller formaten. Ospecificerad kodning behandlas som UTF8.

När TVSDK identifierar ID3-metadata skickas ett meddelande med följande data:

* InfoCode = 303007
* TYPE = ID3
* NAME = finns inte
* ID = 0

1. Implementera en händelseavlyssnare för `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` och registrera det med `MediaPlayer` -objekt.

   TVSDK anropar den här avlyssnaren när ID3-metadata identifieras.

   >[!NOTE]
   >
   >Anpassade annonser använder samma `onTimedMetadata` -händelse för att indikera identifiering av en ny tagg. Detta bör inte skapa någon förvirring eftersom anpassade annonser identifieras på manifestnivå och ID3-taggar bäddas in i strömmen. Mer information finns i custom-tags-configure.

1. Hämta metadata.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
