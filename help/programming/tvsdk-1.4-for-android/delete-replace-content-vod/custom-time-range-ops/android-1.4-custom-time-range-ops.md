---
description: TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.
title: Anpassade åtgärder för tidsintervall
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Anpassade åtgärder för tidsintervall {#custom-time-range-operations}

TVSDK stöder programmatisk borttagning och ersättning av annonsinnehåll i VOD-strömmar.

Funktionen för att ta bort och ersätta utökar funktionen för anpassade annonsmarkörer. Anpassade annonsmärken markerar delar av huvudinnehållet som annonsrelaterade innehållsperioder. Förutom att markera dessa tidsintervall kan du även ta bort och ersätta tidsintervall.

Borttagning och ersättning av annonser implementeras med `TimeRange`-element som identifierar olika typer av tidsintervall i en VOD-ström: markera, ta bort och ersätta. För var och en av dessa anpassade tidintervalltyper kan du utföra motsvarande åtgärder, inklusive att ta bort och ersätta annonsinnehåll.

TVSDK använder följande *anpassade tidsintervallåtgärder*-lägen för att ta bort och ersätta annonser:

* **MARK**
(Dessa kallades anpassade annonsmärken i tidigare versioner av TVSDK). De anger start- och sluttider för annonser som redan har placerats i VOD-strömmen. När det finns tidsintervallmarkörer av typen MARK i strömmen, är den inledande placeringen av 
`Mode.MARK` genereras och löses av  `CustomAdMarkersContentResolver`. Inga annonser infogas.

* **Tidsintervall**
för DELETEF eller DELETE, en inledande 
`placementInformation` av typen  `Mode.DELETE` skapas och löses av motsvarande  `DeleteContentResolver`. `ContentRemoval` är en ny  `timelineOperation` som definierar de intervall som ska tas bort från tidslinjen. TVSDK använder `removeByLocalTime` från AVE-API:t (Adobe Video Engine) för att underlätta den åtgärden. Om det finns DELETE-intervall och Adobe Primetime-annonsbeslutsmetadata (som tidigare kallades Auditude) tas intervallen bort först, och `AuditudeResolver` löser annonserna med det normala arbetsflödet för Adobe Primetime annonsbeslut.

* **Tidsintervall**
FÖR REPLACEF eller REPLACE, två inledande 
`placementInformations` skapas, en  `Mode.DELETE` och en  `Mode.REPLACE`. `DeleteContentResolver` tar bort tidsintervallen först och sedan infogar `AuditudeResolver` annonser av den angivna `replaceDuration` på tidslinjen. Om ingen `replaceDuration` har angetts avgör servern vad som ska infogas.

TVSDK ger stöd för dessa anpassade åtgärder för tidsintervall genom att tillhandahålla följande:

* Flera innehållslösningar

   En ström kan ha flera innehållslösningar som baseras på annonssignaleringsläget och annonsmetadata. Beteendet ändras med olika kombinationer av annonseringssignaleringslägen och annonsmetadata.
* Flera initiala `PlacementInformations` `DefaultMediaPlayer` skapar en lista med initiala `PlacementInformations` baserat på annonseringssigneringsläget och lägger till metadata som ska matchas av `MediaPlayerClient`.

* Nytt läge för annonssignalering: Anpassade tidsintervall

   Annonserna placeras baserat på tidsintervalldata från en extern källa (till exempel en JSON-fil).