---
description: MediaPlayer-gränssnittet kapslar in en mediespelares funktioner och beteende.
title: Konfigurera MediaPlayer
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i TVSDK, som har metoder för att spela upp och hantera videoklipp. TVSDK innehåller till exempel metoderna play och pause. Du kan skapa knappar för användargränssnitt på din plattform och ställa in knapparna för att anropa dessa TVSDK-metoder. MediaPlayer-gränssnittet kapslar in funktioner och beteende i en mediespelare.

TVSDK erbjuder en enda implementering av `MediaPlayer` gränssnitt: klassen DefaultMediaPlayer. Instansiera när du behöver videouppspelningsfunktioner `DefaultMediaPlayer`.

>[!NOTE]
>
>Interagera med `DefaultMediaPlayer` endast med metoderna som exponeras av `MediaPlayer` gränssnitt.

1. Instansiera en `MediaPlayerContext` med programinläst `authorizedFeatures` instans (se [Läs in din signerade token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Instansiera en `MediaPlayer` med metoden public create factory, skicka en `MediaPlayerContext` kontextobjekt:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Detta returnerar en allmän `MediaPlayer` gränssnitt. 1. Instansiera en `MediaPlayerView` och ange den StageVideo-instans som ska användas:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associera `MediaPlayerView` -instans med den nya vyn:

   ```
   mediaPlayer.view = view;
   ```

1. Placera `MediaPlayerView` -instans på enhetens skärm:

   ```
   container.addChild(view)
   ```

The `MediaPlayer` -instansen är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.
