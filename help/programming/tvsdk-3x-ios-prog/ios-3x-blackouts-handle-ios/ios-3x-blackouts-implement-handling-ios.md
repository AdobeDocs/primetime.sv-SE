---
description: TVSDK tillhandahåller API:er och exempelkod för hantering av utbrottsperioder.
title: Implementera hantering av strömavbrott
exl-id: 57823364-fdb3-41c3-8441-008e991f19a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Implementera hantering av strömavbrott {#implement-blackout-handling}

TVSDK tillhandahåller API:er och exempelkod för hantering av utbrottsperioder.

Så här implementerar du hantering av strömavbrott och tillhandahåller alternativt innehåll under strömavbrott:

1. Konfigurera din app för att prenumerera på taggar för strömavbrott i ett liveströmmanifest.

   ```
   - (void) createMediaPlayer:(PTMediaPlayerItem *)item 
   { 
       [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:<INSERT-BLACKOUT-TAG>]]; 
       // For example:  
       // [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-OATCLS-SCTE35"]]; 
   }
   ```

1. Lägg till en meddelandeavlyssnare för `PTTimedMetadataChangedNotification`.

   ```
   - (void)addobservers 
   { 
       [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerSubscribedTagIdentified:)  
         name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
   }
   ```

1. Implementera en avlyssnarmetod för `PTTimedMetadata` objekt i förgrunden.

   Till exempel:

   ```
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]  
         retain]; 
   
    if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
        // handle tag. For example: store it in a dictionary keyed by time to be handled when  
        //   playback time = timedMetadata time. 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. Handtag `TimedMetadata` objekt med konstanta uppdateringar under uppspelningen.

   ```
   - (void)onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       @synchronized(self) 
       { 
           CMTimeRange seekableRange = self.player.seekableRange; 
           if (CMTIMERANGE_IS_VALID(seekableRange)) 
           { 
               _currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
               if (isnan(_currentTime)) 
               { 
                   _currentTime = 0; 
               } 
               [self handleCollectionAtTime:_currentTime]; 
           } 
       } 
   }
   ```

1. Lägg till `PTTimedMetadata` -hanterare för att växla till alternativt innehåll och återgå till huvudinnehållet som anges av `PTTimedMetadata` objekt och dess uppspelningstid.

   ```
   - (void)handleCollectionAtTime:(int)currentTime 
   { 
       NSArray *allKeys = nil; 
       NSMutableArray * timedMetadatasToDelete = [[[NSMutableArray alloc]init]autorelease]; 
   
       if (!_inBlackout && timedMetadataCollection) 
       { 
           allKeys = [timedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
   
               if (currentTime == [currTimedMetadataTime integerValue] &&  
                                  currTimedMetadata.name == <INSERT-BLACKOUT-TAG> &&  
                                  [self isBlackoutStart: currTimedMetadata]) 
               { 
                                   PTAdMetadata *newItemAdMetadata =  
                                     [self createAlternateMediaMetadata];            
   
               // 1. Turn off preroll on the alternate media item. 
                   newItemAdMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *newItem =  
                                 [[PTMediaPlayerItem alloc]initWithUrl: 
                                   <INSERT-ALTERNATE-STREAM-URL mediaId:<INSERT-ALTERNATE-STREAM- 
                                    MEDIA-ID> metadata:newItemAdMetadata];
   
              // 2. Register the current (original playback item) in background. 
                   [self.player registerCurrentItemAsBackgroundItem]; 
   
              // 3. Replace the current playback item with the alternate stream. 
                    [self.player replaceCurrentItemWithPlayerItem:newItem]; 
   
              // 4. Reset observers. 
                   [self removeObservers]; 
                   [self addobservers]; 
   
              // 5. Register listener on the subscribed tags in background item. 
                   [[NSNotificationCenter defaultCenter] addObserver:self  
                      selector:@selector(onSubscribedTagInBackground:)  
                       name:PTTimedMetadataChangedInBackgroundNotification  
                         object:self.player.currentItem]; 
   
              // 6. Register listener on the error in background item. 
                            [[NSNotificationCenter defaultCenter]  
                               addObserver:self selector:@selector(onBackgroundManifestError:)  
                               name:PTBackgroundManifestErrorNotification   
                                 object:self.player.currentItem]; 
   
              // 7. Resume playback 
                        [self.player play]; 
   
                       // 8. Set boolean to true to handle blackout end. 
                     _inBlackout = YES; 
                     break; 
               } 
           } 
       } 
       else if (_inBlackout && backgroundTimedMetadataCollection) 
       { 
           allKeys = [backgroundTimedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [backgroundTimedMetadataCollection objectForKey:allKeys[i]]; 
   
               if (currentTime == ([currTimedMetadataTime integerValue] &&  
                 currTimedMetadata.name == <INSERT-BLACKOUT-TAG>  &&  
                 [self isBlackoutEnd:currTimedMetadata] ) 
               {      
                                  // 1. Come out of blackout. Unregister background item. 
                              [self.player unregisterCurrenBackgroundItem]; 
   
                       PTMetadata *metadata = [self createMetadata]; 
                       PTAdMetadata *adMetadata =  
                         (PTAdMetadata *)[currMetadata metadataForKey:PTAdResolvingMetadataKey]; 
                             adMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *item =  
                                 [[[PTMediaPlayerItem alloc] initWithUrl:<INSERT-ORIGINAL-URL>  
                                   mediaId:<INSERT-ORIGINAL-MEDIAID> metadata:metadata autorelease]; 
   
                                   // 2. Switch back to original item. 
                       [self.player replaceCurrentItemWithPlayerItem:item]; 
                       self.player.autoPlay = YES; 
                       [self removeObservers]; 
   
                       // 3. Remove background item listener. 
                       [[NSNotificationCenter defaultCenter] removeObserver:self  
                          name:PTTimedMetadataChangedInBackgroundNotification  
                       object:self.player.currentItem]; 
   
                                  [[NSNotificationCenter defaultCenter] removeObserver:self  
                                     name:PTBackgroundManifestErrorNotification 
                       object:self.player.currentItem]; 
                       [self addobservers]; 
                       [self.player play]; 
   
                               // 4. Update boolean to correctly maintain the current state. 
                       _inBlackout = NO; 
                       break; 
               } 
           } 
       } 
   }
   ```

1. Implementera en avlyssnarmetod för `PTTimedMetadata` objekt i bakgrunden.

   ```
   - (void)onSubscribedTagInBackground:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *) 
         [userInfo objectForKey:PTTimedMetadataKey] retain]; 
   
       if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [backgroundTimedMetadataCollection  
              setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. Implementera en avlyssnarmetod för bakgrundsfel.

   ```
   - (void) onBackgroundManifestError:(NSNotification *)notification 
   { 
       NSLog (@"onBackgroundManifestError"); 
   }
   ```

1. Om det svarta området finns på DVR-skivan i uppspelningsströmmen uppdaterar du de icke sökbara intervallen.

   ```
   // This sample assumes that blackoutStartTimedMetadata is the PTTimedMetadata  
   // object that indicated "blackout start", and assuming blackoutEndTimedMetadata is the  
   // PTTimedMetadataObject that indicated "blackout end". Since in this case they are both  
   // in DVR, both are notified to the application before playback starts. This is the right  
   // time for the application to set this range in DVR as non-seekable range. 
   
   CMTime ignoreRangeStart = blackoutStartTimedMetadata.time; 
   CMTime ignoreRangeDuration = CMTimeMakeWithSeconds(CMTimeMakeWithSeconds  
     (CMTimeGetSeconds(blackoutEndTimedMetadata.time) -   
        CMTimeGetSeconds(blackoutStartTimedMetadata.time)),  
          blackoutEndTimedMetadata.time.timescale); 
   
   CMTimeRange ignoreRange = CMTimeRangeMake(ignoreRangeStart, ignoreRangeDuration); 
   NSArray *ignoreRangeArray = [NSArray arrayWithObject:[NSValue valueWithCMTimeRange:ignoreRange]]; 
   PTBlackoutMetadata *blackoutMetadata =  
     [[PTBlackoutMetadata alloc]initWithNonSeekableRanges:ignoreRangeArray]; 
   PTMetadata *currMetadata = self.item.metadata; 
   
   if (currMetadata) 
   { 
       [currMetadata setMetadata:blackoutMetadata forKey:PTBlackoutMetadataKey] 
   }
   ```
