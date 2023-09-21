---
description: MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.
title: Konfigurera MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

MediaPlayer-gränssnittet för Android kapslar in en mediespelares funktioner och beteende.

TVSDK erbjuder en implementering av `MediaPlayer` -gränssnittet `DefaultMediaPlayer` klassen. När du behöver videouppspelningsfunktioner ska du instansiera `DefaultMediaPlayer`.

>[!TIP]
>
>Interagera med `DefaultMediaPlayer` endast med de metoder som exponeras av `MediaPlayer` gränssnitt.

1. Instansiera en MediaPlayer med publika `DefaultMediaPlayer.create` standardmetod, skicka ett Java Android-programkontextobjekt.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Utlysning `MediaPlayer.getView` för att få en referens till `MediaPlayerView` -instans.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Placera `MediaPlayerView` -instans i en `FrameLayout` -instans som placerar videon på enhetens skärm.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

The `MediaPlayer` -instansen är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.
