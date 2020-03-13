---
description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-title: Få tillgång till alternativa ljudspår
title: Få tillgång till alternativa ljudspår
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills `MediaPlayer` statusen är minst `MediaPlayerStatus.PREPARED` angiven.
1. Lyssna efter `MediaPlayerEvent.STATUS_CHANGED` händelsen med status `MediaPlayerStatus.PREPARED`.

   Det här steget innebär att den inledande listan med ljudspår är tillgänglig.

1. Hämta tillgängliga ljudspår från `MediaPlayerItem` instansen.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `MediaPlayerItem` instansen.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
