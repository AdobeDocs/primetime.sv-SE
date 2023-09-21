---
description: Händelsehanterare gör att Browser TVSDK kan svara på händelser.
title: Implementera händelseavlyssnare och återanrop
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

   * **Andra händelser**: Valfritt, beroende på vilket program du använder.

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
