---
description: Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i ett VOD-strömsmärke, ta bort och ersätt. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.
title: Anpassade åtgärder för tidsintervall
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Anpassade åtgärder för tidsintervall {#custom-time-range-operations}

Klassen CustomRangeMetadata identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

TVSDK använder följande *anpassade tidsintervallåtgärder*-lägen för att ta bort och ersätta annonser:

* **** MARKTDetta läge kallades för anpassade annonsmärken i tidigare versioner av TVSDK. Läget anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen `MARK` i strömmen skapas en inledande placering av `Mode.MARK` av `CustomMarkerOpportunityGenerator` och löses av `CustomRangeResolver`. Inga annonser infogas.

* **** DELETEF, eller  `DELETE` tidsintervall,  `placementInformation` skapas och löses en början  `Mode.DELETE` av typen  `CustomRangeResolver`. `DeleteRangeTimelineOperation` definierar de intervall som ska tas bort från tidslinjen, och TVSDK använder API:t för videomotorn (AVE)  `removeByLocalTime` från Adobe för att slutföra åtgärden. Om det finns DELETE-intervall och Adobe Primetime-metadata för annonsbeslut tas intervallen bort först, så löser `AuditudeResolver` annonserna med hjälp av det typiska arbetsflödet för Adobe Primetime-annonsbeslut.

* **** REPLACEF `REPLACE` eller tidsintervall  `placementInformations` skapas två initialer, ett  `Mode.DELETE` och ett  `Mode.REPLACE`. `CustomRangeResolver` tar bort tidsintervallen först och sedan  `AuditudeResolver` infogar annonser för det angivna  `replaceDuration` i tidslinjen. Om ingen `replaceDuration` har angetts avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

   En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Flera initiala möjligheter med `CustomMarkerOpportunityGenerator`.
* Ett nytt annonseringssignaleringsläge, `CUSTOM_RANGES`.

   Annonserna placeras baserat på tidsintervalldata från en extern källa, till exempel en JSON-fil.