---
description: Skapa en PlaybackManager som hanterar konfigurationen och uppspelningen av HLS-strömmen. Ingen annan konfiguration krävs.
title: Aktivera videouppspelning
exl-id: b53f602b-5752-4471-9905-2e4351dfc8d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Aktivera videouppspelning {#enable-video-playback}

Skapa en PlaybackManager som hanterar konfigurationen och uppspelningen av HLS-strömmen. Ingen annan konfiguration krävs.

1. Skapa mediespelarobjektet genom att kontrollera att följande kod finns i [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. Skapa uppspelningshanteraren via `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. Implementera `PlaybackManagerEventListener` i `PlayerFragment` för att hantera uppspelningshändelser:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. Registrera händelseavlyssnaren i `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. Ställ in videoresursen:

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. Ställ in åtgärder för kontrollfältet i `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## Relaterad API-dokumentation {#related-api-documentation}

* [Klassen PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)
