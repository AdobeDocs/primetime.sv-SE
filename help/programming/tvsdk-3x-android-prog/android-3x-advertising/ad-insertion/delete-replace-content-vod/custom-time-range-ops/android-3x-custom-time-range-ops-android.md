---
description: Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i ett VOD-strömsmärke, ta bort och ersätt. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.
seo-description: Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i ett VOD-strömsmärke, ta bort och ersätt. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.
seo-title: Anpassade åtgärder för tidsintervall
title: Anpassade åtgärder för tidsintervall
uuid: eadd4d8d-0e03-40ca-ae3b-eede82bf2df8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Anpassade åtgärder för tidsintervall {#custom-time-range-operations}

Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

För borttagning och ersättning av annonser använder TVSDK följande *anpassade åtgärdslägen* för tidsintervall:

* **MARK** Det här läget kallades för anpassade annonsmarkörer i tidigare versioner av TVSDK. Läget anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen `MARK` i strömmen skapas en inledande placering av `Mode.MARK` av `CustomMarkerOpportunityGenerator` och löses av `CustomRangeResolver`. Inga annonser infogas.

* **DELETE** För `DELETE` tidsintervall skapas en början `placementInformation` av typen `Mode.DELETE` och löses av `CustomRangeResolver`. `DeleteRangeTimelineOperation` definierar de intervall som ska tas bort från tidslinjen, och TVSDK använder API:t `removeByLocalTime` för Adobe Video Engine (AVE) för att slutföra den här åtgärden. Om det finns DELETE-intervall och Adobe Primetime-metadata för annonsbeslut, tas intervallen bort först, och annonserna `AuditudeResolver` löses sedan med hjälp av det vanliga arbetsflödet för annonsbeslut i Adobe Primetime.

* **ERSÄTT** För `REPLACE` tidsintervall `placementInformations` skapas två initialer, ett `Mode.DELETE` och ett `Mode.REPLACE`. `CustomRangeResolver` tar bort tidsintervallen först och sedan `AuditudeResolver` infogar annonser för det angivna `replaceDuration` i tidslinjen. Om inget `replaceDuration` anges avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

   En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Flera initiala möjligheter med `CustomMarkerOpportunityGenerator`.
* Ett nytt läge för annonssignalering, `CUSTOM_RANGES`.

   Annonserna placeras baserat på tidsintervalldata från en extern källa, till exempel en JSON-fil.