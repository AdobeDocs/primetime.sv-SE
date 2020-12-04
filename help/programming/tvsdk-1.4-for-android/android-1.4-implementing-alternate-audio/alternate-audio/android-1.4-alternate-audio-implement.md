---
description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-description: Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.
seo-title: Få tillgång till alternativa ljudspår
title: Få tillgång till alternativa ljudspår
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Åtkomst till alternativa ljudspår{#access-alternate-audio-tracks}

Ljud med låg bindning använder MediaPlayer för att spela upp en video som har angetts i en HLS-spellista för M3U8 och som kan innehålla flera alternativa ljudströmmar.

1. Vänta tills MediaPlayer är i åtminstone tillståndet PREPARED.
1. Lyssna efter den här händelsen:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: Den inledande listan med ljudspår är tillgänglig.

1. Hämta tillgängliga ljudspår från `MediaPlayerItem`-instansen.

   `mediaPlayerItem.getAudioTracks()` 1. (Valfritt) Visa tillgängliga spår för användaren.
1. Ställ in det valda ljudspåret på `MediaPlayerItem`-instansen.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`