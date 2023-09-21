---
description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
title: Visa undertexter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Visa undertexter {#expose-subtitles}

TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.

Du kommer åt tillgängliga undertexter via `PTMediaPlayerItem` egenskapens `subtitlesOptions`.

Visa undertexter:

1. Registrera klienten som avlyssnare för `PTMediaPlayerMediaSelectionOptionsAvailableNotification` meddelande.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   När din kund får det här meddelandet är undertexterna klara i `PTMediaPlayerItem`.
1. Implementera `onMediaPlayerItemMediaSelectionOptionsAvailable` metod som liknar följande exempel:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Mer information om alternativa ljudspår finns i  [Alternativt ljud](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
