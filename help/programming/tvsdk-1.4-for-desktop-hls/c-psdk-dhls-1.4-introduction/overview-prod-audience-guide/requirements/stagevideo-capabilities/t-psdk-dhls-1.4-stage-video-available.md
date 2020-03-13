---
description: Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.
seo-description: Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.
seo-title: Kontrollera om StageVideo är tillgängligt
title: Kontrollera om StageVideo är tillgängligt
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Kontrollera om StageVideo är tillgängligt{#check-whether-stagevideo-is-available}

Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.

Från och med Flash 15 återgår maskinvaran till programvara när maskinvaran inte `StageVideo` är tillgänglig `StageVideo`. I Flash 14 och tidigare kan du avgöra om det `StageVideo` är tillgängligt eller inte. Om `StageVideo` inte är tillgängligt kan du använda för `StageVideoAvailabilityEvent` att förstå varför det inte är tillgängligt.

1. Lyssna efter `StageVideoAvailabilityEvent` för att avgöra om `StageVideo` är tillgängligt.

   Exempel:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Om `StageVideo` inte är tillgängligt kontrollerar du `flash.media.StageVideoAvailabilityReason`.
