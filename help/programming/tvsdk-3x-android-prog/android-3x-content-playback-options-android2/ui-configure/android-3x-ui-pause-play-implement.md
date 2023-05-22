---
description: Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.
title: Spela upp och pausa en video
exl-id: 7084ef55-4da6-48af-9951-5360bad7bfa9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Spela upp och pausa en video {#play-and-pause-a-video}

Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.

1. Så här skapar du en paus- eller uppspelningsknapp:
   1. Vänta tills spelaren har förberetts.
   1. Om du vill starta uppspelningen anropar du `play` metod:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Om du vill pausa uppspelningen anropar du `pause()` metod:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Använd återanrop om statusändring för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet `pause()` eller `play()` och skickar information om statusändringen, inklusive den nya statusen, till exempel pausad eller uppspelning.
