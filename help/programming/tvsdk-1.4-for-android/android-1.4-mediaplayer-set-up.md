---
description: MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.
seo-description: MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.
seo-title: Konfigurera MediaPlayer
title: Konfigurera MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.

TVSDK erbjuder en implementering av gränssnittet `MediaPlayer`, klassen `DefaultMediaPlayer`. Instansiera `DefaultMediaPlayer` när du behöver videouppspelningsfunktioner.

>[!TIP]
>
>Interagera med `DefaultMediaPlayer`-instansen endast med de metoder som visas i `MediaPlayer`-gränssnittet.

1. Skapa en MediaPlayer med den offentliga standardmetoden `DefaultMediaPlayer.create` och skicka ett kontextobjekt för Java Android-program.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Anropa `MediaPlayer.getView` för att hämta en referens till `MediaPlayerView`-instansen.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Placera `MediaPlayerView`-instansen i en `FrameLayout`-instans, som placerar videon på enhetens skärm.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

Instansen `MediaPlayer` är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.
