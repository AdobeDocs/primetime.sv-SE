---
description: Meddelandedelen i webbläsarens TVSDK-bibliotek gör att du kan skapa ett loggnings- och felsökningssystem som kan vara användbart för diagnostik och validering.
seo-description: Meddelandedelen i webbläsarens TVSDK-bibliotek gör att du kan skapa ett loggnings- och felsökningssystem som kan vara användbart för diagnostik och validering.
seo-title: Meddelandesystem
title: Meddelandesystem
uuid: 69c4ff1d-3167-413b-ab49-942a5ddc34d7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Meddelandesystem {#notification-system}

Meddelandedelen i webbläsarens TVSDK-bibliotek gör att du kan skapa ett loggnings- och felsökningssystem som kan vara användbart för diagnostik och validering.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Webbläsarens TVSDK har en *no throw* -princip för dess API. De flesta metoder returnerar ett `PSDKErrorCode` värde som anger om metoden kördes utan fel. En fullständig lista över alla möjliga `PSDKErrorCode` värden finns i Webbläsarens TVSDK API-referenser.

Asynkrona fel meddelas via specifika händelser.

Webbläsarens TVSDK skickar `MediaPlayer` händelser för att ge information om spelaraktivitet. Du måste implementera händelseavlyssnare för att hämta och svara på dessa händelser.

>[!TIP]
>
>Viktiga händelser och information loggas på webbläsarkonsolen.

## Lyssna efter meddelanden {#section_06B96633433D497E842FB7ADD5F2C7DA}

Du kan lyssna efter meddelanden och lägga till egna meddelanden i meddelandehistoriken. Kärnan i webbläsarens TVSDK-meddelandesystem är `Notification` klassen, som representerar ett fristående meddelande.

Så här ställer du in programmet så att det lyssnar efter meddelanden:

1. Lyssna efter statusändringar för MediaPlayer genom att använda MediaPlayer-instansen.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementera återanropet.

   Callback-funktionen tar emot en instans av `AdobePSDK.MediaPlayerStatusChangeEvent`och Browser TVSDK skickar händelseobjektet till callback-funktionen som innehåller det nya spelarläget.
1. Ditt program kan lyssna på andra händelser som skickas av Browser TVSDK med hjälp av `MediaPlayer` instansen.

