---
description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
title: Lös och infoga Live/linear-annonser
exl-id: 2097520f-283b-4839-af5e-b1cfb0f3f359
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Lösa och infoga Live/linear-annonser {#resolve-and-insert-live-linear-ad}

För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

TVSDK infogar annonser på följande sätt:

* **Före rullning**, som placeras före innehållet.
* **Mid-roll**, som placeras mitt i innehållet.

TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har TVSDK stöd för `#EXT-X-CUE` som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` värde som ska uttryckas i sekunder och referensens unika ID. Till exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Du kan definiera och abonnera på ytterligare kommandon (taggar).

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierades i manifestet. När annonserna har lösts och infogats beräknar TVSDK den virtuella tidslinjen igen och skickar en `TimelineItemsUpdatedEventListener.onTimelineUpdated` -händelse.
