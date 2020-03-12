---
description: Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.
seo-description: Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Konfigurera felhantering{#set-up-error-handling}

Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.

1. Lägg till en händelseavlyssnare för `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Exempel:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. I händelseavlyssnaren anger du den logik som ska användas för att hantera alla fel när `event.status` den är `AdobePSDK.MediaPlayerStatus.ERROR`.
1. Återställ objektet eller läs in en ny medieresurs när felet har hanterats. `MediaPlayer`

       När MediaPlayer-objektet är i feltillstånd kan det inte avsluta det här läget förrän du utför någon av följande åtgärder:
   
   * Återställ MediaPlayer-objektet med hjälp av `MediaPlayer.reset` metoden.
   * Läs in en ny medieresurs med `MediaPlayer.replaceCurrentResource` metoden .

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

Exempel:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```

