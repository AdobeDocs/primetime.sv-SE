---
description: 'null'
seo-description: 'null'
seo-title: Markera intervall
title: Markera intervall
uuid: 994a8f07-0951-47ec-b21a-d74c9eeefd74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Markera intervall{#mark-ranges}

Så här implementerar du `PTTimeRangeCollection` och markerar innehållsområden som annonser:
1. Förbered `PTTimeRangeCollection`den.
1. Ange typen för `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeMarkRanges`.

   I det här steget meddelas TVSDK om att anpassade intervall måste behandlas som annonser.

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
       type:PTTimeRangeCollectionTypeMarkRanges];
   ```

1. Skapa `PTAdMetadata` och ställ in `PTTimeRangeCollection`.

   ```
   // Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   // Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

1. Skapa spelaren och starta uppspelningen.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```

## Ersätt intervall{#replace-ranges}

Så här implementerar du `PTTimeRangeCollection` och tar bort innehållsintervall som annonser:
1. Förbered `PTTimeRangeCollection`.
1. Ange typen för `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeReplaceRanges`.

   I det här steget meddelas TVSDK om att de angivna intervallen måste ersättas med alternativt innehåll (annonser).

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)] 
                       ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeReplaceRanges];
   ```

   >[!TIP]
   >
   >Argumentet `replacementDuration` är valfritt. Om det inte är definierat `AdServer` avgör annonsbrytningens varaktighet.

1. Skapa `PTAdMetadata` och ställ in `PTTimeRangeCollection`.

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeCustomRanges; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >Även om inställningen `signalingMode` är inställd som `PTAdSignalingModeCustomRanges`, ställs det här annonseringsläget in automatiskt när du ställer in `PTTimeRangeCollection` typen `PTTimeRangeCollectionTypeReplace`.

1. Skapa spelaren och starta uppspelningen.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```

## Ta bort intervall {#delete-ranges}

Så här implementerar du `PTTimeRangeCollection` och tar bort innehållsintervall som annonser:
1. Förbered `PTTimeRangeCollection`den.
1. Ange typen för `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeDeleteRanges`, som meddelar TVSDK om att de angivna intervallen måste tas bort.

   ```
   #define PSDK_TIMESCALE 100000 
   
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
   
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeDeleteRanges];
   ```

1. Skapa `PTAdMetadata` och ställ in `PTTimeRangeCollection`.

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
   
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeServerMap; 
   
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >Annonsinfogning sker efter att de anpassade intervallen har tagits bort baserat på `PTAdMetadata` och aktuell `PTAdSignalingMode`.

1. Skapa spelaren och starta uppspelningen.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```
