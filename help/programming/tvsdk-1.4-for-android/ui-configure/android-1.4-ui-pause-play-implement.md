---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
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

1. Använd `MediaPlayer.PlaybackEventListener.onStateChanged` återanrop för att söka efter fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om lägesändringen i återanropet, inklusive det nya läget, som PAUSED eller PLAYING.
