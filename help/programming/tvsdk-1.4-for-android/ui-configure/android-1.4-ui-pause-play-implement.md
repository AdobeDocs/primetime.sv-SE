---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
seo-description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
seo-title: Spela upp och pausa en video
title: Spela upp och pausa en video
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Spela upp och pausa en video{#play-and-pause-a-video}

Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.

1. Skapa en paus-/uppspelningsknapp som gör följande.
   1. Vänta tills spelaren är i åtminstone tillståndet PREPARED.
   1. Om du vill starta uppspelningen anropar du TVSDK-uppspelningsmetoden:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Om du vill pausa uppspelningen anropar du TVSDK-pausmetoden:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Använd `MediaPlayer.PlaybackEventListener.onStateChanged`-återanropet för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om lägesändringen i återanropet, inklusive det nya läget, som PAUSED eller PLAYING.

