---
description: Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.
title: Kontrollera om StageVideo är tillgängligt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Kontrollera om StageVideo är tillgängligt{#check-whether-stagevideo-is-available}

Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.

Från Flash 15 och senare, när maskinvara `StageVideo` är inte tillgängligt, kommer programmet att återgå till `StageVideo`. För Flash 14 och tidigare kan du ange om `StageVideo` är tillgängligt. If `StageVideo` är inte tillgängligt, du kan använda `StageVideoAvailabilityEvent` för att förstå varför det inte är tillgängligt.

1. Lyssna efter `StageVideoAvailabilityEvent` för att avgöra om `StageVideo` är tillgängligt.

   Till exempel:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. If `StageVideo` är inte tillgänglig, kontrollera `flash.media.StageVideoAvailabilityReason`.
