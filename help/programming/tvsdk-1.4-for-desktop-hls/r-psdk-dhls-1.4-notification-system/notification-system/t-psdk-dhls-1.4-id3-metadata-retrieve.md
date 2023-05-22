---
description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. identifierar ID3-taggar på segmentnivå för transportström (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
title: ID3-taggar
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# ID3-taggar{#id-tags}

ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. identifierar ID3-taggar på segmentnivå för transportström (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.

>[!IMPORTANT]
>
>TVSDK känner igen ID3-metadata (version 2.3.0 eller 2.4.0) i ljud- (AAC) och videoströmmar (H.264) i någon av dess möjliga kodningar (ASCII, UTF8, UTF16-BE eller UTF16-LE). Den ignorerar ID3-taggar som inte finns i någon av de godkända versionerna eller formaten. Ospecificerad kodning behandlas som UTF8.

När TVSDK identifierar ID3-metadata skickas ett meddelande med följande data:

* InfoCode = 303007
* TYPE = ID3
* NAME = finns inte
* ID = 0

1. Implementera en händelseavlyssnare för `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` och registrera det med `MediaPlayer` -objekt.

   TVSDK anropar den här avlyssnaren när ID3-metadata identifieras.

   >[!NOTE]
   >
   >Anpassade annonser använder samma `onTimedMetadata` -händelse för att indikera identifiering av en ny tagg. Detta bör inte skapa någon förvirring eftersom anpassade annonser identifieras på manifestnivå och ID3-taggar bäddas in i strömmen. Mer information finns i custom-tags-configure.

1. Hämta metadata.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```
