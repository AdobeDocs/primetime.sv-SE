---
description: Du kan lägga till webbläsarens TVSDK-beteende för att pausa och spela upp knappar.
title: Spela upp och pausa en video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

1. Lyssna på `AdobePSDK.MediaPlayerStatusChangeEvent` händelse för att kontrollera om det finns fel eller för att vidta andra lämpliga åtgärder.

   Browser TVSDK utlöser den här händelsen när metoderna för paus eller uppspelning anropas och skickar information om händelseobjektet, inklusive det nya läget, som `MediaPlayerStatus.PLAYING` eller `MediaPlayerStatus.PAUSED`.
