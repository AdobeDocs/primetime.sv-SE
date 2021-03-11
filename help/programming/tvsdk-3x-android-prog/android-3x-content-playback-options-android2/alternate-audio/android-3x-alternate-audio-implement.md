---
description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Åtkomst till alternativa ljudspår{#access-alternate-audio-tracks}

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
