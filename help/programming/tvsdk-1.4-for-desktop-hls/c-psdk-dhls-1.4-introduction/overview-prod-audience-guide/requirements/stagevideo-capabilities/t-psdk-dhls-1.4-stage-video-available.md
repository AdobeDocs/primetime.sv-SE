---
description: Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.
title: Kontrollera om StageVideo är tillgängligt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Kontrollera om StageVideo är tillgängligt{#check-whether-stagevideo-is-available}

Om StageVideo inte är tillgängligt och programmet försöker använda StageVideo, genererar inte TVSDK något fel. Programmet kan avgöra om StageVideo är tillgängligt genom att avlyssna StageVideoAvailabilityEvent.

Från Flash 15 och senare, när maskinvaran `StageVideo` inte är tillgänglig, återgår den till programvara `StageVideo`. För Flash 14 och tidigare kan du avgöra om `StageVideo` är tillgängligt. Om `StageVideo` inte är tillgängligt kan du använda `StageVideoAvailabilityEvent` för att förstå varför det inte är tillgängligt.

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
