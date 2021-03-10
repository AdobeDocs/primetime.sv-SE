---
description: För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
title: Lösning och infogning av annonser live/linjärt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Lösning och infogning av annonser - live/linjär{#live-linear-ad-resolving-and-insertion}

För direktsänt/linjärt innehåll ersätter TVSDK en del av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

TVSDK infogar annonser på följande sätt:

* **Pre-roll**, som är i början av innehållet.
* **Mid-roll**, som är mitt i innehållet.

TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard stöder TVSDK `#EXT-X-CUE`-referensen som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` i sekunder och referensens unika ID. Exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>När du implementerar en anpassad `AdPolicySelector` kan en annan princip ges för pre-roll, mid-roll och post-roll `AdBreakTimelineItem`s i `AdPolicyInfo`, vilket baseras på typen av `AdBreakTimelineItem`s. Du kan t.ex. behålla innehåll i mitten av rullen efter att det har spelats upp, men ta bort innehåll före uppspelning.

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierades i manifestet. När annonserna har lösts och infogats beräknar TVSDK den virtuella tidslinjen igen och skickar en `TimelineEvent.TIMELINE_UPDATED`-händelse.
