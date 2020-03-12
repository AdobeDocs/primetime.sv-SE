---
description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-title: Lösning och infogning av annonser live/linjärt
title: Lösning och infogning av annonser live/linjärt
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Lösning och infogning av annonser live/linjärt{#live-linear-ad-resolving-and-insertion}

För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

TVSDK infogar annonser på följande sätt:

* **Pre-roll**, som är i början av innehållet.
* **Mid-roll**, som är mitt i innehållet.

TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har TVSDK stöd för `#EXT-X-CUE` referenspunkten som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` i sekunder och referensens unika ID. Exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>När man implementerar en sedvanlig regel `AdPolicySelector`kan man ge en annan policy för förrullning, mellanrullning och efterrullning `AdBreakTimelineItem`i `AdPolicyInfo`som baseras på typen av `AdBreakTimelineItem`s. Du kan t.ex. behålla innehåll i mitten av rullen efter att det har spelats upp, men ta bort innehåll före uppspelning.

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierades i manifestet. När annonserna har lösts och infogats beräknar TVSDK den virtuella tidslinjen igen och skickar en `TimelineEvent.TIMELINE_UPDATED` händelse.
