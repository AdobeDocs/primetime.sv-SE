---
description: Händelsehanterare gör att Browser TVSDK kan svara på händelser.
seo-description: Händelsehanterare gör att Browser TVSDK kan svara på händelser.
seo-title: Implementera händelseavlyssnare och återanrop
title: Implementera händelseavlyssnare och återanrop
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%

---


# Implementera händelseavlyssnare och återanrop{#implement-event-listeners-and-callbacks}

Händelsehanterare gör att Browser TVSDK kan svara på händelser.

När en händelse inträffar anropar en webbläsares TVSDK-händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen till hanteraren.

Ditt program måste implementera händelseavlyssnare för Browser TVSDK-händelser som påverkar ditt program.

1. Avgör för vilka händelser ditt program måste avlyssna.

   * **Nödvändiga händelser**: Lyssna efter alla uppspelningshändelser.

      >[!IMPORTANT]
      >
      >Uppspelningshändelsen `STATUS_CHANGED` anger spelarläget, inklusive fel. Alla lägen kan påverka spelarens nästa steg.

   * **Andra händelser**: Valfritt, beroende på ditt program.

      Om du till exempel inkluderar annonsering i uppspelningen lyssnar du efter alla `AdBreakPlaybackEvent`- och `AdPlaybackEvent`-händelser.

1. Implementera händelseavlyssnare för varje händelse.

   Webbläsarens TVSDK returnerar parametervärden till händelseavlyssnarens återanrop. Dessa värden ger relevant information om händelsen som du kan använda i dina avlyssnare för att utföra lämpliga åtgärder.

   Exempel:

   * Händelsetyp: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Händelseegenskap: `MediaPlayerStatus.<event>` används så här:

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. Registrera dina callback-avlyssnare med `MediaPlayer`-objektet med `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
