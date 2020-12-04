---
description: Skapa en PlaybackManager som hanterar konfigurationen och uppspelningen av HLS-strömmen. Ingen annan konfiguration krävs.
seo-description: Skapa en PlaybackManager som hanterar konfigurationen och uppspelningen av HLS-strömmen. Ingen annan konfiguration krävs.
seo-title: Aktivera videouppspelning
title: Aktivera videouppspelning
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '185'
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

1. Implementera `PlaybackManagerEventListener` i `PlayerFragment` för att hantera uppspelningshändelserna:

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