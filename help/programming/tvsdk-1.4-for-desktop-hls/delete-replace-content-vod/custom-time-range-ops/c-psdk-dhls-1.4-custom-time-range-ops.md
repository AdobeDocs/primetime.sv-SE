---
description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
title: Anpassade åtgärder för tidsintervall
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Översikt {#custom-time-range-operations-overview}

TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.

Funktionen för att ta bort och ersätta utökar funktionen för anpassade annonsmarkörer. Anpassade annonsmärken markerar delar av huvudinnehållet som annonsrelaterade innehållsperioder. Förutom att markera dessa tidsintervall kan du även ta bort och ersätta tidsintervall.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

Borttagning och ersättning av annonser implementeras med anpassade markörer som identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För varje anpassat tidsintervall kan du utföra associerade åtgärder, som att ta bort eller ersätta annonsinnehåll.

TVSDK innehåller följande *anpassade åtgärder för tidsintervall* för att ta bort och ersätta annonser:

* MARK - Skickar `AdBreak`-händelser för de markerade regionerna. (Detta kallades `customAdMarker` i tidigare versioner av TVSDK.) Annonsinfogning tillåts inte i det här läget.

* DELETE - I det här läget använder programmet klassen `TimeRangeCollection` för att definiera tidsregioner för C3 Ad Deletion. Annonsinfogning tillåts i det här läget.
* REPLACE - I det här läget ersätter programmet en `timeRange` med ett Adobe Primetime-annonsbeslut `AdBreak`. Ersättningsåtgärden startar där C3 Ad-borttagningen sker och slutar vid den angivna tiden (kortare eller längre än det ursprungliga tidsintervallet).

TVSDK erbjuder en `CustomRangesOpportunityGenerator`-klass för att generera placeringsmöjligheter för intervallen MARK och DELETE. I REPLACE-läget genererar TVSDK två placeringsmöjligheter för varje tidsintervall:

* `CustomRangeResolver` genererar placeringsmöjligheter för DELETE
* `AuditudeAdResolver` genererar placeringsmöjligheter för INSERT.