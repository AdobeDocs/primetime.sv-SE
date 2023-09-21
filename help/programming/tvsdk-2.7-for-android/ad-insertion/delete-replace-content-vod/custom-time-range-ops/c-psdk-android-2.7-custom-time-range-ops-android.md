---
description: Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i ett VOD-strömsmärke, ta bort och ersätt. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.
title: Anpassade åtgärder för tidsintervall
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Ökning {#custom-time-range-operations}

Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i en VOD-ström: mark, delete och replace. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

TVSDK använder följande för att ta bort och ersätta annonser *anpassad åtgärd för tidsintervall* lägen:

* **MARK** Det här läget kallades för anpassade annonsmarkörer i tidigare versioner av TVSDK. Läget anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen `MARK` i flödet, en inledande placering av `Mode.MARK` genereras av `CustomMarkerOpportunityGenerator` och löses av `CustomRangeResolver`. Inga annonser infogas.

* **DELETE** För `DELETE` tidsintervall, en initial `placementInformation` av typen `Mode.DELETE` skapas och löses av `CustomRangeResolver`. `DeleteRangeTimelineOperation` definierar de intervall som ska tas bort från tidslinjen, och TVSDK använder `removeByLocalTime` från AVE-API:t (Adobe Video Engine) för att slutföra åtgärden. Om det finns DELETE-intervall och Adobe Primetime-metadata för annonsbeslut tas intervallen bort först, sedan visas `AuditudeResolver` löser annonser med hjälp av det typiska arbetsflödet för Adobe Primetime-annonsbeslut.

* **ERSÄTT** För `REPLACE` tidsintervall, två initiala `placementInformations` skapas, en `Mode.DELETE` och en `Mode.REPLACE`. `CustomRangeResolver` tar bort tidsintervallen först och sedan `AuditudeResolver` infogar annonser av den angivna `replaceDuration` till tidslinjen. Om nej `replaceDuration` anges avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

  En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Flera initiala möjligheter med `CustomMarkerOpportunityGenerator`.
* Ett nytt signaleringsläge, `CUSTOM_RANGES`.

  Annonserna placeras baserat på tidsintervalldata från en extern källa, till exempel en JSON-fil.
