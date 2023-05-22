---
description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta på `MediaPlayer` vara i åtminstone statusen FÖRBEREDD.
1. Lyssna efter dessa händelser:

   * `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med ljudspår är tillgänglig.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Ljudspår som ändrats under uppspelning

1. Hämta tillgängliga ljudspår från `MediaPlayerItem` -instans.
1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ange det valda ljudspåret på `MediaPlayerItem` -instans.
