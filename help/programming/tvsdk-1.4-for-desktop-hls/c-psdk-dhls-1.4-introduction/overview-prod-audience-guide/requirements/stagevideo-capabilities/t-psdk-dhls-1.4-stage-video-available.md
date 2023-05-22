---
description: Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.
title: Kontrollera om StageVideo är tillgängligt
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
