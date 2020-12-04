---
description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
seo-description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
seo-title: Visa undertexter
title: Visa undertexter
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Visa underrubriker {#expose-subtitles}

TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.

Du kommer åt tillgängliga undertexter via `PTMediaPlayerItem`-egenskapens `subtitlesOptions`.

Visa undertexter:

1. Registrera klienten som avlyssnare för `PTMediaPlayerMediaSelectionOptionsAvailableNotification`-meddelandet.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   När klienten får det här meddelandet är undertexterna klara i `PTMediaPlayerItem`.
1. Implementera metoden `onMediaPlayerItemMediaSelectionOptionsAvailable` som i följande exempel:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Mer information om alternativa ljudspår finns i [Alternativt ljud](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).