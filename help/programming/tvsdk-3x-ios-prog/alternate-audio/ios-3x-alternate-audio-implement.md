---
description: Ljud med låg bindning använder PTMediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-description: Ljud med låg bindning använder PTMediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-title: Få tillgång till alternativa ljudspår
title: Få tillgång till alternativa ljudspår
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Åtkomst till alternativa ljudspår {#access-alternate-audio-tracks}

Ljud med låg bindning använder PTMediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills MediaPlayer har minst statusen `PTMediaPlayerStatusReady`.
1. Lyssna efter den här händelsen:

   meddelande `PTMediaPlayerItemMediaSelectionOptionsAvailable`: Den inledande listan med ljudspår är tillgänglig.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Hämta tillgängliga ljudspår från `PTMediaPlayerItem`-instansen.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `PTMediaPlayerItem`-instansen.
