---
description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
title: Lösning och infogning av annonser live/linjärt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Lösning och infogning av annonser live/linjärt{#live-linear-ad-resolving-and-insertion}

För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

TVSDK infogar annonser på följande sätt:

* **Före rullning**, som är i början av innehållet.
* **Mid-roll**, som är mitt i innehållet.

TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har TVSDK stöd för `#EXT-X-CUE` som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` på några sekunder och referensens unika ID. Till exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>Vid implementering av en standard `AdPolicySelector`kan en annan policy ges för förrullning, mellanrullning och efterrullning `AdBreakTimelineItem`s in `AdPolicyInfo`, som baseras på typen av `AdBreakTimelineItem`s. Du kan t.ex. behålla innehåll i mellanrullen efter att det har spelats upp, men ta bort innehåll i pre-roll efter att det har spelats upp.

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierades i manifestet. När annonserna har lösts och infogats beräknar TVSDK den virtuella tidslinjen igen och skickar en `TimelineEvent.TIMELINE_UPDATED` -händelse.
