---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
seo-description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
seo-title: Spela upp och pausa en video
title: Spela upp och pausa en video
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Spela upp och pausa en video{#play-and-pause-a-video}

Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.

1. Skapa en paus-/uppspelningsknapp som gör följande.
   1. Vänta tills spelaren har statusen PREPARED.
   1. Om du vill starta uppspelningen anropar du TVSDK-uppspelningsmetoden:

      ```
      function play():void;
      ```

   1. Om du vill pausa uppspelningen anropar du TVSDK-pausmetoden:

      ```
      function pause():void;
      ```

1. Använd callback-funktionen för `MediaPlayerStatusChangeEvent.STATUS_CHANGED` händelsen för att söka efter fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om statusändringen i återanropet, inklusive den nya statusen, som PAUSED eller PLAYING.
