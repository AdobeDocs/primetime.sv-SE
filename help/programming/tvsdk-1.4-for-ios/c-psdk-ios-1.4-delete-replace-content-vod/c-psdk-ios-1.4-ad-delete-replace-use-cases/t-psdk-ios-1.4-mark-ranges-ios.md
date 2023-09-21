---
title: Markera intervall
description: Markera intervall
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Markera intervall{#mark-ranges}

Så här implementerar du `PTTimeRangeCollection` och markera innehållsområden som annonser:
1. Förbered `PTTimeRangeCollection`.
1. Ange typ av `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeMarkRanges`.

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

1. Skapa `PTAdMetadata` och ange `PTTimeRangeCollection`.

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

Så här implementerar du `PTTimeRangeCollection` och radera innehållsintervall som annonser:
1. Förbered `PTTimeRangeCollection`.
1. Ange typ av `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeReplaceRanges`.

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
   >Argumentet `replacementDuration` är valfritt. Om den inte är definierad `AdServer` Anger längden på annonsbrytningen.

1. Skapa `PTAdMetadata` och ange `PTTimeRangeCollection`.

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
   >Även om `signalingMode` anges som `PTAdSignalingModeCustomRanges`, ställs det här annonseringssigneringsläget in automatiskt när inställningen för `PTTimeRangeCollection` av typen `PTTimeRangeCollectionTypeReplace`.

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

Så här implementerar du `PTTimeRangeCollection` och radera innehållsintervall som annonser:
1. Förbered `PTTimeRangeCollection`.
1. Ange typ av `PTTimeRangeCollection` till `PTTimeRangeCollectionTypeDeleteRanges`, som meddelar TVSDK om att de angivna intervallen måste tas bort.

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

1. Skapa `PTAdMetadata` och ange `PTTimeRangeCollection`.

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
   >Annonsinfogning sker efter att de anpassade intervallen har tagits bort baserat på `PTAdMetadata` och den aktuella `PTAdSignalingMode`.

1. Skapa spelaren och starta uppspelningen.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
   
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
   
   //Start playback 
   [player play];
   ```
