---
description: TVSDK meddelar spelarklienten om att det finns interna AVAsset-objekt tillgängligaMediaCharacpropertiesWithMediaSelectionOptions med hjälp av PTMediaPlayerMediaSelectionOptionsAvailableNotification-meddelandet.
title: Visa undertexter
exl-id: dc726a5b-2eab-4ebd-8773-7396bf818205
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
