---
description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
title: Få tillgång till alternativa ljudspår
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Få tillgång till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills MediaPlayer är i åtminstone tillståndet PREPARED.
1. Lyssna efter den här händelsen:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: Den inledande listan med ljudspår är tillgänglig.

1. Hämta tillgängliga ljudspår från `MediaPlayerItem` -instans.

   `mediaPlayerItem.getAudioTracks()` 1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ange det valda ljudspåret på `MediaPlayerItem` -instans.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
