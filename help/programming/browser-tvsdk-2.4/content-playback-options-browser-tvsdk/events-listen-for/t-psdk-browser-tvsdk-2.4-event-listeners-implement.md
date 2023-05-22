---
description: Händelsehanterare gör att Browser TVSDK kan svara på händelser.
title: Implementera händelseavlyssnare och återanrop
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Implementera händelseavlyssnare och återanrop{#implement-event-listeners-and-callbacks}

Händelsehanterare gör att Browser TVSDK kan svara på händelser.

När en händelse inträffar anropar en webbläsares TVSDK-händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen till hanteraren.

Ditt program måste implementera händelseavlyssnare för Browser TVSDK-händelser som påverkar ditt program.

1. Avgör för vilka händelser ditt program måste avlyssna.

   * **Nödvändiga händelser**: Lyssna efter alla uppspelningshändelser.

      >[!IMPORTANT]
      >
      >Uppspelningshändelsen `STATUS_CHANGED` innehåller spelarstatus, inklusive fel. Alla lägen kan påverka spelarens nästa steg.

   * **Andra händelser**: Valfritt, beroende på ditt program.

      Om du till exempel inkluderar annonsering i uppspelningen lyssnar du efter alla `AdBreakPlaybackEvent` och `AdPlaybackEvent` händelser.

1. Implementera händelseavlyssnare för varje händelse.

   Webbläsarens TVSDK returnerar parametervärden till händelseavlyssnarens återanrop. Dessa värden ger relevant information om händelsen som du kan använda i dina avlyssnare för att utföra lämpliga åtgärder.

   Till exempel:

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

1. Registrera dina callback-avlyssnare med `MediaPlayer` objekt genom att använda `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
