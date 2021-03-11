---
description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Åtkomst till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills `MediaPlayer` har statusen PREPARED.
1. Lyssna efter dessa händelser:

   * `MediaPlayerItemEvent.ITEM_CREATED`: Den inledande listan med ljudspår är tillgänglig.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Ljudspår som ändrats under uppspelning

1. Hämta tillgängliga ljudspår från `MediaPlayerItem`-instansen.
1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `MediaPlayerItem`-instansen.
