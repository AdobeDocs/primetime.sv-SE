---
description: Du kan lägga till webbläsarens TVSDK-beteende för att pausa och spela upp knappar.
seo-description: Du kan lägga till webbläsarens TVSDK-beteende för att pausa och spela upp knappar.
seo-title: Spela upp och pausa en video
title: Spela upp och pausa en video
uuid: 4053ea9e-6b74-41e9-ad04-087ad13e3698
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Spela upp och pausa en video{#play-and-pause-a-video}

Du kan lägga till webbläsarens TVSDK-beteende för att pausa och spela upp knappar.

1. Skapa en paus-/uppspelningsknapp som gör följande.
   1. Vänta tills spelaren är i åtminstone tillståndet PREPARED.
   1. Om du vill starta uppspelningen anropar du uppspelningsmetoden i webbläsaren TVSDK:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Om du vill pausa uppspelningen anropar du webbläsarens TVSDK-pausmetod:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Lyssna efter `AdobePSDK.MediaPlayerStatusChangeEvent` händelsen för att söka efter fel eller för att vidta andra lämpliga åtgärder.

   Webbläsarens TVSDK utlöser den här händelsen när metoderna för paus eller uppspelning anropas och skickar information om händelseobjektet, inklusive det nya läget, som `MediaPlayerStatus.PLAYING` eller `MediaPlayerStatus.PAUSED`.

