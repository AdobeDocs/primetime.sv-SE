---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

1. Använd `MediaPlayer.PlaybackEventListener.onStateChanged` återanrop för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om lägesändringen i återanropet, inklusive det nya läget, som PAUSED eller PLAYING.
