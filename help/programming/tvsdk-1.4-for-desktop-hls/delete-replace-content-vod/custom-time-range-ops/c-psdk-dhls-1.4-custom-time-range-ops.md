---
description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
seo-description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
seo-title: Anpassade åtgärder för tidsintervall
title: Anpassade åtgärder för tidsintervall
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Översikt {#custom-time-range-operations-overview}

TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.

Funktionen för att ta bort och ersätta utökar funktionen för anpassade annonsmarkörer. Anpassade annonsmärken markerar delar av huvudinnehållet som annonsrelaterade innehållsperioder. Förutom att markera dessa tidsintervall kan du även ta bort och ersätta tidsintervall.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

Borttagning och ersättning av annonser implementeras med anpassade markörer som identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För varje anpassat tidsintervall kan du utföra associerade åtgärder, som att ta bort eller ersätta annonsinnehåll.

För borttagning och ersättning av annonser innehåller TVSDK följande lägen för *anpassade tidsintervallåtgärder* :

* MARK - Skickar `AdBreak` händelser för de markerade områdena. (Detta kallades `customAdMarker` i tidigare versioner av TVSDK.) Annonsinfogning tillåts inte i det här läget.

* DELETE - I det här läget använder programmet `TimeRangeCollection` klassen för att definiera tidsregioner för C3 Ad Deletion. Annonsinfogning tillåts i det här läget.
* REPLACE - I det här läget ersätter appen en `timeRange` med ett Adobe Primetime-annonsbeslut `AdBreak`. Ersättningsåtgärden startar där C3 Ad-borttagningen sker och slutar vid den angivna tiden (kortare eller längre än det ursprungliga tidsintervallet).

TVSDK erbjuder en `CustomRangesOpportunityGenerator` klass för att generera placeringsmöjligheter för intervallen MARK och DELETE. I REPLACE-läget genererar TVSDK två placeringsmöjligheter för varje tidsintervall:

* Det `CustomRangeResolver` genererar placeringsmöjligheter för DELETE
* Här `AuditudeAdResolver` genereras placeringsmöjligheter för INSERT.