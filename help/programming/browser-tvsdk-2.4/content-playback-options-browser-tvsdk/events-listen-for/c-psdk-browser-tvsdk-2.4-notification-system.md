---
description: Meddelandedelen i webbläsarens TVSDK-bibliotek gör att du kan skapa ett loggnings- och felsökningssystem som kan vara användbart för diagnostik och validering.
title: Meddelandesystem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Meddelandesystem {#notification-system}

Meddelandedelen i webbläsarens TVSDK-bibliotek gör att du kan skapa ett loggnings- och felsökningssystem som kan vara användbart för diagnostik och validering.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Webbläsaren TVSDK har en *ingen throw* princip för dess API. De flesta metoder returnerar en `PSDKErrorCode` värde för att ange om metoden har körts. För en fullständig lista över alla möjliga `PSDKErrorCode` värden, se Webbläsare-TVSDK API-referenser.

Asynkrona fel meddelas via specifika händelser.

Webbläsarens TVSDK-utskick `MediaPlayer` händelser för att ge information om spelaraktivitet. Du måste implementera händelseavlyssnare för att kunna hämta och svara på dessa händelser.

>[!TIP]
>
>Viktiga händelser och information loggas på webbläsarkonsolen.

## Lyssna efter meddelanden {#section_06B96633433D497E842FB7ADD5F2C7DA}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken. Kärnan i meddelandesystemet för webbläsare-TVSDK är `Notification` -klass, som representerar ett fristående meddelande.

Så här ställer du in programmet så att det lyssnar efter meddelanden:

1. Lyssna efter statusändringar för MediaPlayer genom att använda MediaPlayer-instansen.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementera återanropet.

   Återanropet tar emot en instans av `AdobePSDK.MediaPlayerStatusChangeEvent`och Browser TVSDK skickar händelseobjektet till återanropet som innehåller det nya spelarläget.
1. Ditt program kan lyssna på andra händelser som skickas av Browser TVSDK med `MediaPlayer` -instans.
