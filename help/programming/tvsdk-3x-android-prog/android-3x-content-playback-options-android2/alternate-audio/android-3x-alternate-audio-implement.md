---
description: Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Alternativt ljud använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta på `MediaPlayer` att vara i åtminstone `MediaPlayerStatus.PREPARED` status.
1. Lyssna på `MediaPlayerEvent.STATUS_CHANGED` händelse med status `MediaPlayerStatus.PREPARED`.

   Det här steget innebär att den inledande listan med ljudspår är tillgänglig.

1. Hämta tillgängliga ljudspår från `MediaPlayerItem` -instans.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ange det valda ljudspåret på `MediaPlayerItem` -instans.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
