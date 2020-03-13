---
description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-title: Få tillgång till alternativa ljudspår
title: Få tillgång till alternativa ljudspår
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills `MediaPlayer` statusen PREPARED är minst.
1. Lyssna efter dessa händelser:

   * `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med ljudspår är tillgänglig.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Ljudspår som ändrats under uppspelning

1. Hämta tillgängliga ljudspår från `MediaPlayerItem` instansen.
1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `MediaPlayerItem` instansen.
