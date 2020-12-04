---
description: Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.
seo-description: Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.
seo-title: Lägga till avlyssnare för meddelanden om tidsbestämda metadata
title: Lägga till avlyssnare för meddelanden om tidsbestämda metadata
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Lägg till avlyssnare för meddelanden om tidsbestämda metadata{#add-listeners-for-timed-metadata-notifications}

Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.

När ett nytt `TimedMetadata`-objekt skapas skickar MediaPlayer `AdobePSDK.TimedMetadataEvent`.

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

ID3-metadata skickas via samma `Events.TimedMetadataEvent`. Du kan använda egenskapen `timedMetadata.type` för att skilja mellan TAGG och ID3.

