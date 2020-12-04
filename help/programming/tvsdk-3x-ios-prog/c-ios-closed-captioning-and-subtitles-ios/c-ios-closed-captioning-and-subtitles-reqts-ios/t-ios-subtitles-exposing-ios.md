---
description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
seo-description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
seo-title: Visa undertexter
title: Visa undertexter
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
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

   Mer information om alternativa ljudspår finns i [Alternativt ljud](../../alternate-audio/ios-3x-alternate-audio.md).