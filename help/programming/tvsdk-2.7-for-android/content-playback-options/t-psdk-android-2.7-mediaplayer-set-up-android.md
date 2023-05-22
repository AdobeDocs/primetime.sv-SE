---
description: Skapa en instans av en MediaPlayer och placera en vy av den i en bildrutelayout.
title: Konfigurera MediaPlayer
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Konfigurera MediaPlayer {#set-up-the-mediaplayer}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.

Skapa en instans av en MediaPlayer och placera en vy av den i en bildrutelayout.

1. Instansiera `MediaPlayer`, skicka ett `android.content.Context` objekt till konstruktorn:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Ange en ramlayout ( `android.widget.FrameLayout`) för att hålla `ViewGroup` av `mediaPlayer`:

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

1. Placera en vy över `mediaPlayer` inuti ramlayouten:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>The `MediaPlayer` instans ( `mediaPlayer`) är nu tillgängligt och korrekt konfigurerat för att visa videoinnehåll på enhetsskärmen.
