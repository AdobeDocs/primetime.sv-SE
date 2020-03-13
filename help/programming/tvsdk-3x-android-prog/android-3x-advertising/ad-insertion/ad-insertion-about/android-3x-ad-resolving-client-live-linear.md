---
description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-title: Lös och infoga Live/linear-annonser
title: Lös och infoga Live/linear-annonser
uuid: 722569f2-d260-4fcc-b6b9-01d86aa00e28
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Lösa och infoga Live/linear-annonser {#resolve-and-insert-live-linear-ad}

För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

TVSDK infogar annonser på följande sätt:

* **Pre-roll**, som placeras före innehållet.
* **Mid-roll**, som placeras mitt i innehållet.

TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har TVSDK stöd för `#EXT-X-CUE` referenspunkten som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver att metadatafältet `DURATION` uttrycks i sekunder och att referensens unika ID anges. Exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Du kan definiera och abonnera på ytterligare kommandon (taggar).

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierades i manifestet. När annonserna har lösts och infogats beräknar TVSDK den virtuella tidslinjen igen och skickar en `TimelineItemsUpdatedEventListener.onTimelineUpdated` händelse.