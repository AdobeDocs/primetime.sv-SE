---
description: Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.
title: Använd tidsbestämda metadata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Använd tidsbestämda metadata {#use-timed-metadata}

Du kan använda TimedMetadata när den aktuella uppspelningstiden matchar starttiden.

Om du vill använda dessa sparade `PTTimedMetadata`-objekt under uppspelning använder du den sparade ordlistan från [Lagra tidsbestämda metadataobjekt när de skickas](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Extrahera och uppdatera den aktuella uppspelningstiden från det här meddelandet och hitta alla `PTTimedMetadata`-objekt med starttider som matchar den aktuella uppspelningstiden.

   Du kan använda dessa objekt för att slutföra olika åtgärder.

   Exempel:

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. Justera regelbundet inaktuella `PTTimedMetadata`-instanser från listan för att förhindra att minnet växer kontinuerligt.