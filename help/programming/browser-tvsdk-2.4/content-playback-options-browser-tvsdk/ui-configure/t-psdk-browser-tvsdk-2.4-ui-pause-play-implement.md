---
description: Du kan lägga till webbläsarens TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

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

1. Lyssna efter händelsen `AdobePSDK.MediaPlayerStatusChangeEvent` om du vill söka efter fel eller vidta andra lämpliga åtgärder.

   Webbläsarens TVSDK utlöser den här händelsen när metoderna för att pausa eller spela upp anropas och skickar information om händelseobjektet, inklusive det nya läget, till exempel `MediaPlayerStatus.PLAYING` eller `MediaPlayerStatus.PAUSED`.

