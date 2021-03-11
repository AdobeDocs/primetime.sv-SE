---
description: TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.
title: Konfigurera mediespelaren
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Konfigurera mediespelaren {#set-up-the-media-player}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Skapa en `MediaPlayer`-instans och placera en vy av den i en ramlayout.

1. Instansiera `MediaPlayer` och skicka ett `android.content.Context`-objekt till konstruktorn:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Ange en bildrutelayout ( `android.widget.FrameLayout`) för en `ViewGroup` av `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >Nedan visas kodfragmentet som ska skapas `_viewGroup`.

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

   >[!NOTE]
   >
   >`MediaPlayer`-instansen ( `mediaPlayer`) är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.