---
description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. identifierar ID3-taggar på segmentnivå för transportström (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. identifierar ID3-taggar på segmentnivå för transportström (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-title: ID3-taggar
title: ID3-taggar
uuid: 5c016260-5ced-480e-897a-11ffe7f34441
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '283'
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

1. Implementera en händelseavlyssnare för `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` och registrera den med objektet `MediaPlayer`.

   TVSDK anropar den här avlyssnaren när ID3-metadata identifieras.

   >[!NOTE]
   >
   >Anpassade annonsinställningar använder samma `onTimedMetadata`-händelse för att ange identifiering av en ny tagg. Detta bör inte skapa någon förvirring eftersom anpassade annonser identifieras på manifestnivå och ID3-taggar bäddas in i strömmen. Mer information finns i custom-tags-configure.

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

