---
description: Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.
title: Konfigurera felhantering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Konfigurera felhantering{#set-up-error-handling}

Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.

1. Lägga till en händelseavlyssnare för `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Till exempel:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. I händelseavlyssnaren, när `event.status` är `AdobePSDK.MediaPlayerStatus.ERROR`, innehåller den logik som behövs för att hantera alla fel.
1. När felet har hanterats återställer du `MediaPlayer` eller läsa in en ny medieresurs.

       När MediaPlayer-objektet är i feltillstånd kan det inte avsluta det här läget förrän du utför någon av följande åtgärder:
   
   * Återställ MediaPlayer-objektet med `MediaPlayer.reset` -metod.
   * Läs in en ny medieresurs med `MediaPlayer.replaceCurrentResource` -metod.

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

Till exempel:

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
