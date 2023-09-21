---
description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
title: Anpassade åtgärder för tidsintervall
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Anpassade åtgärder för tidsintervall {#custom-time-range-operations}

TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.

Funktionen för att ta bort och ersätta utökar funktionen för anpassade annonsmarkörer. Anpassade annonsmärken markerar delar av huvudinnehållet som annonsrelaterade innehållsperioder. Förutom att markera dessa tidsintervall kan du även ta bort och ersätta tidsintervall.

Borttagning och ersättning av annonser implementeras med `TimeRange` element som identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

TVSDK använder följande för att ta bort och ersätta annonser *anpassad åtgärd för tidsintervall* lägen:

* **MARK**
(Dessa kallades anpassade annonsmarkörer i tidigare versioner av TVSDK). De anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen MARK i strömmen, är den inledande placeringen av `Mode.MARK` genereras och löses av `CustomAdMarkersContentResolver`. Inga annonser infogas.

* **DELETE**
För tidsintervall i DELETE, en inledande `placementInformation` av typen `Mode.DELETE` skapas och löses av motsvarande `DeleteContentResolver`. `ContentRemoval` är en ny `timelineOperation` som definierar de intervall som ska tas bort från tidslinjen. TVSDK använder `removeByLocalTime` från Adobe Video Engine (AVE) API för att underlätta denna operation. Om det finns DELETE-intervall och Adobe Primetime-annonsmetadata (som tidigare kallades Auditude), tas intervallen bort först och sedan tas `AuditudeResolver` löser annonser med hjälp av det normala arbetsflödet för annonsbeslut i Adobe Primetime.

* **ERSÄTT**
För REPLACE-tidsintervall gäller två initiala `placementInformations` skapas, en `Mode.DELETE` och en `Mode.REPLACE`. The `DeleteContentResolver` tar bort tidsintervallen först och sedan `AuditudeResolver` infogar annonser av den angivna `replaceDuration` till tidslinjen. Om nej `replaceDuration` anges avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

  En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Flera initialer `PlacementInformations` The `DefaultMediaPlayer` skapar en lista med inledande `PlacementInformations` baserat på annonssignaleringsläget och annonseringsmetadata som ska lösas av `MediaPlayerClient`.

* Nytt läge för annonssignering: Anpassade tidsintervall

  Annonserna placeras baserat på tidsintervalldata från en extern källa (till exempel en JSON-fil).
