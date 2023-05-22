---
description: Du kan lägga till TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

1. Använd motringning för `MediaPlayerStatusChangeEvent.STATUS_CHANGED` händelse för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet när pause- eller play-metoden anropas. TVSDK skickar information om statusändringen i återanropet, inklusive den nya statusen, som PAUSED eller PLAYING.
