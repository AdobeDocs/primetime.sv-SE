---
description: Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.
title: Lägga till avlyssnare för meddelanden om tidsbestämda metadata
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Lägga till avlyssnare för meddelanden om tidsbestämda metadata{#add-listeners-for-timed-metadata-notifications}

Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.

När en ny `TimedMetadata` skapas skickas MediaPlayer `AdobePSDK.TimedMetadataEvent`.

1. Implementera lämpliga avlyssnare.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registrera händelseavlyssnarna.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3-metadata skickas via samma `Events.TimedMetadataEvent`. Du kan använda `timedMetadata.type` -egenskap för att skilja mellan TAGG och ID3.
