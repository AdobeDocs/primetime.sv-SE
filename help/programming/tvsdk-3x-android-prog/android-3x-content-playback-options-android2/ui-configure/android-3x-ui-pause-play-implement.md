---
description: Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.
title: Spela upp och pausa en video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Spela upp och pausa en video {#play-and-pause-a-video}

Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.

1. Så här skapar du en paus- eller uppspelningsknapp:
   1. Vänta tills spelaren har förberetts.
   1. Om du vill starta uppspelningen anropar du metoden `play`:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Om du vill pausa uppspelningen anropar du metoden `pause()`:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Använd återanrop om statusändring för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet för `pause()` eller `play()` och skickar information om statusändringen, inklusive den nya statusen, till exempel pausad eller uppspelning.