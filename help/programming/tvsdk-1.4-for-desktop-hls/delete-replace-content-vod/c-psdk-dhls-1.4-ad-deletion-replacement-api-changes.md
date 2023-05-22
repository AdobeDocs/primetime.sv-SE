---
description: De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.
title: Ändringar i API:t för borttagning och ersättning av annonser
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Ändringar i API:t för borttagning och ersättning av annonser {#ad-deletion-and-replacement-api-changes}

De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Tillagd `CUSTOM_RANGES` signaleringsläge.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Uppsättning `AdSignalingMode.CUSTOM_RANGES` om ersättningsintervall finns i metadata.

* `PlacementType` Tillagd `CUSTOM_RANGE` typ.

* `PlacementMode`

   * Tillagd `DELETE` läge.
   * Tillagd `MARK` läge
   * Tillagd `FreeReplace` läge - Det här läget har en varaktighet men är en ren infogning

* `TimeRange` Inte längre en `final` class

* Tillagd `ReplaceTimeRange()` method

   Utökar `TimeRange` att ha `replacementDuration` -egenskap. För MARK och DELETE `replacementDuration` är 0.

* `TimeRangeCollection`

   * Tillagd `toReplaceMetadata()` verktygsfunktion som ska extraheras `timeRanges`.

   * Ändrad att arbeta med `DELETE` och `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Tillagd `createCustomTimeRangesFrom()` - Skapar metadata för JSON-filen för användning av MARK/DELETE/REPLACE.
   * Borttagen `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Tillagd `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Tillagd `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (ändrade inte)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Tillagd `CustomRangesOpportunityGenerator` för när metadata innehåller anpassade intervall
   * `doRetrieveResolvers()`

      * Lägg till `CustomRangeResolver` för när anpassade intervall för DELETE och REPLACE finns i metadata
      * Flyttad `CustomAdMarkerResolver` framför `AuditudeResolver`


* Tillagd `CustomRangeOpportunityGenerator`

   * `doUpdate()` Leaves empty - no Update, VOD
   * `doProcess()` Skapar en ny placering av en ny typ `Placement.Delete_Range`

   * Tillagd `CustomRangeOppotunityGenerator` överst i generatorlistan i `DefaultContentFactory`så att borttagningsintervall behandlas innan annonsinfogningar infogas.

   * Tillagd `createCustomRangeOpportunities` att skapa alla möjligheter

      MARK - en affärsmöjlighet för varje giltigt markeringsintervall för `PlacementType.CUSTOM_RANGE` och `PlacementMode.MARK`

      DELETE - En möjlighet för varje giltigt borttagningsintervall för `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`

      REPLACE - Två möjligheter för varje giltigt ersättningsintervall:

      1. En möjlighet att ta bort intervall från `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`.

      1. Primetimes annonsbeslut och möjlighet att `PlacementType.MID_ROLL` eller `PlacementType.PRE_ROLL` och `PlacementMode.FREEREPLACE`

* Tillagd `CustomRangeResolver`:

   * `doCanResolve()` returnerar `true` för borttagningsintervall.

   * Tillagd `createDeleteRangeOperation()` att skapa `DeleteRange` för placering

* Tillagd `CustomRangeHelper`:

   * Gemensam verktygsklass för att extrahera Mark/Delete/Replace `timeRanges` och bearbeta dem.
   * Tillagd `extractCustomRangesMetadata()`
   * Tillagd `extractCustomRanges()`
   * Tillagd `mergeRanges()` - Löser konflikter och delmängder/sammanfogningar

* `MediaPlayerTimeline`:

   * &quot;>In `executeOperation()`, om åtgärden är `DeleteRange`, lade till anrop till borttagning av metod i åtgärden

   * I `executeOperation()`, om åtgärden är `NOPTimelineOperation` (tom `AdBreaks` kommer tillbaka från servern), lade till anrop för att rensa.

   * Tillagd `onDeleteRangeComplete()`
   * Tillagd `removeRange()`
   * I `adjustPlacement()`, för `PlacementMode.FREEREPLACE` läge, nollställ längden. Den här tidslängden behövs tidigare vid begäran `AdBreaks`måste det nu vara noll för att infogas helt.

* `VideoEngineTimeline` Tillagd `removeC3Ad()` - ring `removeByLocalTime()` för borttagningsintervall

* `AdSignalingModeGenerator`

   * `doConfigure()` - Lös inte om ingen affärsmöjlighet genereras
   * `createInitialOpportunity()` - Generera ingen inledande möjlighet för `AdSignalingMode.CUSTOM_RANGE`. The `CustomRangeOpportunityGenerator` täcker detta redan.

* `DeleteRange`

   * Utökar `TimelineOperation`.
   * Skapad av `CustomRangeResolver` för borttagning och ersättning (borttagningsdelen av ersättningen)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - tillåt paketering
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` The `accepts()` metoden ändrades för att tillåta paketering av olika placeringstyper (före-, mitt- eller efterrullningsläge)

* `AuditudeRequestHelper` Felkorrigeringar som tillåter serveråsidosättning av annonsparametrar

* `AuditudeResolver` The `canBePacked()` metoden ändrades för att tillåta packning

* `CustomAdResolver` The `timeRange` extraheringsfunktionerna har tagits bort. Vi får en placering i taget och gör det till en `AdBreakPlacement timelineOperation`.
