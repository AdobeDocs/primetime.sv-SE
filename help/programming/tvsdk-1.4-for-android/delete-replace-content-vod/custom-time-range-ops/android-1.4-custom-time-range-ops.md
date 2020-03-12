---
description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
seo-description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
seo-title: Anpassade åtgärder för tidsintervall
title: Anpassade åtgärder för tidsintervall
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Anpassade åtgärder för tidsintervall {#custom-time-range-operations}

TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.

Funktionen för att ta bort och ersätta utökar funktionen för anpassade annonsmarkörer. Anpassade annonsmärken markerar delar av huvudinnehållet som annonsrelaterade innehållsperioder. Förutom att markera dessa tidsintervall kan du även ta bort och ersätta tidsintervall.

Borttagning och ersättning av annonser implementeras med `TimeRange` element som identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

För borttagning och ersättning av annonser använder TVSDK följande *anpassade åtgärdslägen* för tidsintervall:

* **MARK**(Dessa kallades anpassade annonsmärken i tidigare versioner av TVSDK). De anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen MARK i strömmen skapas och löses en inledande placering av `Mode.MARK` den av `CustomAdMarkersContentResolver`. Inga annonser infogas.

* **DELETE** För tidsintervallen DELETE `placementInformation` skapas en början `Mode.DELETE` av typen och matchas av motsvarande `DeleteContentResolver`. `ContentRemoval` är ett nytt `timelineOperation` som definierar de intervall som ska tas bort från tidslinjen. TVSDK använder API:t `removeByLocalTime` för Adobe Video Engine (AVE) för att underlätta den åtgärden. Om det finns DELETE-intervall och Adobe Primetime-annonsbeslutsmetadata (tidigare Auditude-metadata), raderas dessa intervall först och annonserna `AuditudeResolver` löses sedan med det normala arbetsflödet för annonseringsbeslut i Adobe Primetime.

* **REPLACE** För REPLACE-tidsintervall `placementInformations` skapas två initialer, ett `Mode.DELETE` och ett `Mode.REPLACE`. Tidsintervallen tas först `DeleteContentResolver` bort och sedan `AuditudeResolver` infogas annonser för det angivna `replaceDuration` i tidslinjen. Om inget `replaceDuration` anges avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

   En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Multiple initial `PlacementInformations` The `DefaultMediaPlayer` skapar en lista med inledande `PlacementInformations` baserat på annonseringssigneringsläget och annonseringsmetadata som ska matchas av `MediaPlayerClient`.

* Nytt läge för annonssignalering: Anpassade tidsintervall

   Annonserna placeras baserat på tidsintervalldata från en extern källa (till exempel en JSON-fil).