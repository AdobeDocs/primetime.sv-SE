---
description: Ljud med låg bindning använder PTMediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
exl-id: f3ab9573-c189-4132-820d-0ce98ee170d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder PTMediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills MediaPlayer finns i åtminstone `PTMediaPlayerStatusReady` status.
1. Lyssna efter den här händelsen:

   meddelande `PTMediaPlayerItemMediaSelectionOptionsAvailable`: Den inledande listan med ljudspår är tillgänglig.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Hämta tillgängliga ljudspår från `PTMediaPlayerItem` -instans.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ange det valda ljudspåret på `PTMediaPlayerItem` -instans.
