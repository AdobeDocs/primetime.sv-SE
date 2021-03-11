---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

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

1. Använd återanropet för händelsen `MediaPlayerStatusChangeEvent.STATUS_CHANGED` om du vill söka efter fel eller vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om statusändringen i återanropet, inklusive den nya statusen, som PAUSED eller PLAYING.
