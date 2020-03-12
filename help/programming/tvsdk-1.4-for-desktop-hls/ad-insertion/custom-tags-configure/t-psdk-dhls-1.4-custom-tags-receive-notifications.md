---
description: Registrera lämplig händelseavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-description: Registrera lämplig händelseavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Lägg till avlyssnare för tidsbestämda metadataaviseringar{#add-listeners-for-timed-metadata-notifications}

Registrera lämplig händelseavlyssnare om du vill få meddelanden om taggar i manifestet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med `TimedMetadata` objekt är tillgänglig när `MediaPlayerItem` de har skapats.

   Den här händelsen meddelar programmet när detta händer.

* `MediaPlayerItemEvent.ITEM_UPDATED`: För live-/linjära strömmar där manifestet/spellistan uppdateras regelbundet kan ytterligare anpassade taggar visas i den uppdaterade spellistan/manifestfilen, så ytterligare `TimedMetadata` objekt kan läggas till i `MediaPlayerItem.timedMetadata` egenskapen.

   Den här händelsen meddelar programmet när detta händer.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Varje gång ett nytt `TimedMetadata` objekt skapas skickas den här händelsen av MediaPlayer.

   Den här händelsen skickas inte för det `TimedMetadata` objekt som skapades under initieringsfasen.

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

ID3-metadata skickas via samma `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Detta bör dock inte skapa någon förvirring eftersom du kan använda ett TimedMetadata-objekts `type` egenskap för att skilja mellan TAGG och ID3. Mer information om ID3-taggar finns i [ID3-taggar](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).