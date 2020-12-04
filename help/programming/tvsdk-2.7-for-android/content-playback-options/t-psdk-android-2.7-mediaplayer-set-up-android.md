---
description: Skapa en instans av en MediaPlayer och placera en vy av den i en bildrutelayout.
seo-description: Skapa en instans av en MediaPlayer och placera en vy av den i en bildrutelayout.
seo-title: Konfigurera MediaPlayer
title: Konfigurera MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.

Skapa en instans av en MediaPlayer och placera en vy av den i en bildrutelayout.

1. Instansiera `MediaPlayer` och skicka ett `android.content.Context`-objekt till konstruktorn:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Ange en bildrutelayout ( `android.widget.FrameLayout`) för en `ViewGroup` av `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   Nedan visas kodfragmentet som ska skapas `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Placera en vy med `mediaPlayer` inuti bildrutelayouten:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>`MediaPlayer`-instansen ( `mediaPlayer`) är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.