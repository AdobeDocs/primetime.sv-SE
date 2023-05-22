---
description: Ljud med sen bindning använder PTMediaPlayer för att spela upp en video som har angetts i en M3U8 HLS-spellista och som kan innehålla flera alternativa ljudströmmar.
title: Åtkomst till alternativa ljudspår
exl-id: c95e2bae-fcf3-4ae2-be11-fb3191b380f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Åtkomst till alternativa ljudspår {#access-alternate-audio-tracks}

Ljud med sen bindning använder PTMediaPlayer för att spela upp en video som har angetts i en M3U8 HLS-spellista och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills MediaPlayer finns i minst `PTMediaPlayerStatusReady` status.
1. Lyssna efter den här händelsen:

   avisering `PTMediaPlayerItemMediaSelectionOptionsAvailable`: Den första listan med ljudspår är tillgänglig.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Hämta de tillgängliga ljudspåren från `PTMediaPlayerItem` -instans.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `PTMediaPlayerItem` -instans.
