---
description: MediaPlayer-gränssnittet kapslar in en mediespelares funktioner och beteende.
seo-description: MediaPlayer-gränssnittet kapslar in en mediespelares funktioner och beteende.
seo-title: Konfigurera MediaPlayer
title: Konfigurera MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i TVSDK, som har metoder för att spela upp och hantera videoklipp. TVSDK innehåller till exempel metoderna play och pause. Du kan skapa knappar för användargränssnitt på din plattform och ställa in knapparna för att anropa dessa TVSDK-metoder. MediaPlayer-gränssnittet kapslar in funktioner och beteende i en mediespelare.

TVSDK erbjuder en enda implementering av gränssnittet `MediaPlayer`: klassen DefaultMediaPlayer. Instansiera `DefaultMediaPlayer` när du behöver videouppspelningsfunktioner.

>[!NOTE]
>
>Interagera med `DefaultMediaPlayer`-instansen endast med de metoder som visas i gränssnittet `MediaPlayer`.

1. Skapa en `MediaPlayerContext`-instans med den programinlästa `authorizedFeatures`-instansen (se [Läs in din signerade token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Skapa en `MediaPlayer`-instans med standardmetoden public, och skicka ett `MediaPlayerContext`-kontextobjekt:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Detta returnerar ett generiskt `MediaPlayer`-gränssnitt. 1. Instansiera en `MediaPlayerView` och ange den StageVideo-instans som ska användas:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associera `MediaPlayerView`-instansen med den nya vyn:

   ```
   mediaPlayer.view = view;
   ```

1. Placera `MediaPlayerView`-instansen på enhetens skärm:

   ```
   container.addChild(view)
   ```

Instansen `MediaPlayer` är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.