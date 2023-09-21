---
description: Registrera lämplig händelseavlyssnare om du vill få meddelanden om taggar i manifestet.
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Lägg till avlyssnare för tidsbestämda metadataaviseringar{#add-listeners-for-timed-metadata-notifications}

Registrera lämplig händelseavlyssnare om du vill få meddelanden om taggar i manifestet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med `TimedMetadata` objekt är tillgängliga efter `MediaPlayerItem` skapas.

  Den här händelsen meddelar programmet när detta händer.

* `MediaPlayerItemEvent.ITEM_UPDATED`: För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestet, så ytterligare `TimedMetadata` kan läggas till i `MediaPlayerItem.timedMetadata` -egenskap.

  Den här händelsen meddelar programmet när detta händer.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Varje gång en ny `TimedMetadata` -objektet skapas, den här händelsen skickas av MediaPlayer.

  Den här händelsen skickas inte för `TimedMetadata` objekt som skapades under initieringsfasen.

1. Implementera lämpliga avlyssnare.

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. Registrera händelseavlyssnarna.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

ID3-metadata skickas via samma `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Detta bör dock inte skapa någon förvirring eftersom du kan använda ett TimedMetadata-objekt `type` för att skilja mellan TAGG och ID3. Mer information om ID3-taggar finns i [ID3-taggar](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
