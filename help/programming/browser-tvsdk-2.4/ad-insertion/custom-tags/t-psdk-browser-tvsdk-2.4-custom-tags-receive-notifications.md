---
description: Om du vill få meddelanden om taggar i manifestet lyssnar du efter AdobePSDK.TimedMetadataEvent.
title: Lägga till avlyssnare för meddelanden om tidsbestämda metadata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
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

