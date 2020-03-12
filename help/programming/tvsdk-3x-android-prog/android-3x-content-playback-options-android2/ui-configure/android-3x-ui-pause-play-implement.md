---
description: Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.
seo-description: Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.
seo-title: Spela upp och pausa en video
title: Spela upp och pausa en video
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Spela upp och pausa en video {#play-and-pause-a-video}

Du kan lägga till paus- och uppspelningsknappar för att pausa eller spela upp videon.

1. Så här skapar du en paus- eller uppspelningsknapp:
   1. Vänta tills spelaren har förberetts.
   1. Om du vill starta uppspelningen anropar du `play` metoden:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Om du vill pausa uppspelningen anropar du `pause()` metoden:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Använd återanrop om statusändring för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   TVSDK anropar det här återanropet för `pause()` eller `play()` skickar information om statusändringen, inklusive den nya statusen, som pausad eller uppspelning.