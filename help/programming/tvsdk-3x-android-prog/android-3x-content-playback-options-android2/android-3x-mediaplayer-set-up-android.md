---
description: TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.
title: Konfigurera mediespelaren
exl-id: 99fdc4c1-0c67-4de5-87a5-b42d76f43ae9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Konfigurera mediespelaren {#set-up-the-media-player}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter. Den innehåller även ett antal funktioner som utformats för att maximera videouppspelningskvaliteten.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Instansiera en `MediaPlayer` och montera en vy av den i en ramlayout.

1. Instansiera `MediaPlayer`, skicka ett `android.content.Context` objekt till konstruktorn:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Ange en ramlayout ( `android.widget.FrameLayout`) för att hålla `ViewGroup` av `mediaPlayer`:

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

1. Placera en vy över `mediaPlayer` inuti ramlayouten:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >The `MediaPlayer` instans ( `mediaPlayer`) är nu tillgängligt och korrekt konfigurerat för att visa videoinnehåll på enhetsskärmen.
