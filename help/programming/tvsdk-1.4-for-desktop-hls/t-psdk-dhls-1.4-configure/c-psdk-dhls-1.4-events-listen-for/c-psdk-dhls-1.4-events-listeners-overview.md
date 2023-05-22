---
description: Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
title: Lyssna efter händelser för Primetime Player
exl-id: 3a740245-a9e1-4e36-8761-f9f4b4e85b93
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Översikt {#implement-event-listeners-and-callbacks-overview}

Händelsehanterare gör att TVSDK kan svara på händelser. När en händelse inträffar anropar TVSDK:s händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen till hanteraren.

Flash Runtime har en generisk händelsemekanism som TVSDK också använder och definierar en serie anpassade händelser. Ditt program måste implementera händelseavlyssnare för TVSDK-händelser som påverkar ditt program.

1. Avgör för vilka händelser ditt program måste avlyssna.

   * **Nödvändiga händelser**: Lyssna efter alla uppspelningshändelser.

      >[!IMPORTANT]
      >
      >Uppspelningshändelsen `MediaPlayerStatusChangeEvent.STATUS_CHANGE` innehåller spelarstatus, inklusive fel. Alla lägen kan påverka spelarens nästa steg.

   * **Andra händelser**: Valfritt, beroende på ditt program.

      Om du till exempel inkluderar annonsering i uppspelningen lyssnar du efter alla `AdBreakPlaybackEvent` och `AdPlaybackEvent` händelser.

1. Implementera händelseavlyssnare för varje händelse.

   TVSDK returnerar parametervärden till återanrop till händelseavlyssnaren. Dessa värden ger relevant information om händelsen som du kan använda i dina avlyssnare för att utföra lämpliga åtgärder.

   The `Event` -klassen visar alla callback-gränssnitt. Varje gränssnitt visar de parametrar som returneras för det gränssnittet.

   Till exempel:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registrera dina callback-avlyssnare med `MediaPlayer` objekt genom att använda `MediaPlayer.addEventListener`.

   `MediaPlayer` extends `flash.events.IEventDispatcher`, som är en del av Flash spelarens kärnfiler och innehåller funktionerna `addEventListener` och `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
