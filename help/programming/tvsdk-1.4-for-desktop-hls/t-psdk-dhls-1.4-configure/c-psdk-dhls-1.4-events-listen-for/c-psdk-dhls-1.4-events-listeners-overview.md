---
description: Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-description: Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-title: Lyssna efter händelser för Primetime Player
title: Lyssna efter händelser för Primetime Player
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Översikt {#implement-event-listeners-and-callbacks-overview}

Händelsehanterare gör att TVSDK kan svara på händelser. När en händelse inträffar anropar TVSDK:s händelsemekanism din registrerade händelsehanterare och skickar händelseinformationen till hanteraren.

Flash Runtime har en generisk händelsemekanism som TVSDK också använder och definierar en serie anpassade händelser. Ditt program måste implementera händelseavlyssnare för TVSDK-händelser som påverkar ditt program.

En fullständig lista över händelser för videoanalys finns i [Spåra grundläggande videouppspelning](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. Avgör för vilka händelser ditt program måste avlyssna.

   * **Nödvändiga händelser**: Lyssna efter alla uppspelningshändelser.

      >[!IMPORTANT]
      >
      >Uppspelningshändelsen `MediaPlayerStatusChangeEvent.STATUS_CHANGE` ger spelarstatus, inklusive fel. Alla lägen kan påverka spelarens nästa steg.

   * **Andra händelser**: Valfritt, beroende på ditt program.

      Om du till exempel inkluderar annonsering i uppspelningen lyssnar du efter alla `AdBreakPlaybackEvent`- och `AdPlaybackEvent`-händelser.

1. Implementera händelseavlyssnare för varje händelse.

   TVSDK returnerar parametervärden till återanrop till händelseavlyssnaren. Dessa värden ger relevant information om händelsen som du kan använda i dina avlyssnare för att utföra lämpliga åtgärder.

   Klassen `Event` visar alla callback-gränssnitt. Varje gränssnitt visar de parametrar som returneras för det gränssnittet.

   Exempel:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registrera dina callback-avlyssnare med `MediaPlayer`-objektet med `MediaPlayer.addEventListener`.

   `MediaPlayer` extends  `flash.events.IEventDispatcher`, som ingår i Flash-spelarens kärnfiler och innehåller funktioner  `addEventListener` och  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


