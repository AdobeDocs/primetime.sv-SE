---
description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-title: Få tillgång till alternativa ljudspår
title: Få tillgång till alternativa ljudspår
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Åtkomst till alternativa ljudspår {#access-alternate-audio-tracks}

Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills `MediaPlayer` har minst statusen `MediaPlayerStatus.PREPARED`.
1. Lyssna efter händelsen `MediaPlayerEvent.STATUS_CHANGED` med statusen `MediaPlayerStatus.PREPARED`.

   Det här steget innebär att den inledande listan med ljudspår är tillgänglig.

1. Hämta tillgängliga ljudspår från `MediaPlayerItem`-instansen.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `MediaPlayerItem`-instansen.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

