---
description: MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.
seo-description: MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.
seo-title: Konfigurera MediaPlayer
title: Konfigurera MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.

TVSDK erbjuder en implementering av `MediaPlayer` gränssnittet, `DefaultMediaPlayer` klassen. Instansiera `DefaultMediaPlayer`när du behöver videouppspelningsfunktioner.

>[!TIP]
>
>Interagera med `DefaultMediaPlayer` instansen endast med de metoder som visas av `MediaPlayer` gränssnittet.

1. Instansiera en MediaPlayer med den publika `DefaultMediaPlayer.create` fabriksmetoden och skicka ett Java Android-programkontextobjekt.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Anropa `MediaPlayer.getView` för att hämta en referens till `MediaPlayerView` instansen.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Placera `MediaPlayerView` instansen i en `FrameLayout` instans som placerar videon på enhetens skärm.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

Instansen är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen. `MediaPlayer`
