---
description: Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.
title: Konfigurera felhantering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 3%

---


# Konfigurera felhantering{#set-up-error-handling}

Du kan konfigurera en plats i programmet för att utföra felhantering som svar på FELtillståndet.

1. Lägg till en händelseavlyssnare för `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Exempel:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. När `event.status` är `AdobePSDK.MediaPlayerStatus.ERROR` i händelseavlyssnaren anger du den logik som ska hantera alla fel.
1. När felet har hanterats återställer du objektet `MediaPlayer` eller läser in en ny medieresurs.

       När MediaPlayer-objektet är i feltillstånd kan det inte avsluta det här läget förrän du utför någon av följande åtgärder:
   
   * Återställ MediaPlayer-objektet med metoden `MediaPlayer.reset`.
   * Läs in en ny medieresurs med metoden `MediaPlayer.replaceCurrentResource`.

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

