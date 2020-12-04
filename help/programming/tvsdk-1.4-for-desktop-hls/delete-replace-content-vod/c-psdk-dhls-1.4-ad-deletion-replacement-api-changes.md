---
description: De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.
seo-description: De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.
seo-title: Ändringar i API:t för borttagning och ersättning av annonser
title: Ändringar i API:t för borttagning och ersättning av annonser
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Ändringar i API:t för borttagning och ersättning av annonser {#ad-deletion-and-replacement-api-changes}

De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Tillagt  `CUSTOM_RANGES` signeringsläge.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Ange  `AdSignalingMode.CUSTOM_RANGES` om ersättningsintervall finns i metadata.

* `PlacementType` Tillagd  `CUSTOM_RANGE` typ.

* `PlacementMode`

   * Läget `DELETE` har lagts till.
   * Läget `MARK` har lagts till
   * Läget `FreeReplace` har lagts till - Det här läget har en varaktighet men är en ren infogning

* `TimeRange` Ingen  `final` klass längre

* Metoden `ReplaceTimeRange()` har lagts till

   Utökar `TimeRange` till att ha en `replacementDuration`-egenskap. För ärenden som rör MARK och DELETE är `replacementDuration` 0.

* `TimeRangeCollection`

   * Verktygsfunktionen `toReplaceMetadata()` har lagts till för att extrahera `timeRanges`.

   * Ändrad att arbeta med `DELETE` och `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Tillagd `createCustomTimeRangesFrom()` - Skapar metadata för användningsfall för MARK/DELETE/REPLACE från JSON-filen.
   * Borttagen `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * `CUSTOM_DELETE_RANGES_METADATA_KEY` har lagts till
   * `CUSTOM_REPLACE_RANGES_METADATA_KEY` har lagts till
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (ändrade inte)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * `CustomRangesOpportunityGenerator` har lagts till när metadata innehåller anpassade intervall
   * `doRetrieveResolvers()`

      * Lägg till `CustomRangeResolver` när anpassade intervall för DELETE och REPLACE finns i metadata
      * Flyttad `CustomAdMarkerResolver` framför `AuditudeResolver`


* `CustomRangeOpportunityGenerator` har lagts till

   * `doUpdate()` Leaves empty - no Update, VOD
   * `doProcess()` Skapar en ny placering av en ny typ  `Placement.Delete_Range`

   * `CustomRangeOppotunityGenerator` har lagts till högst upp i generatorlistan i `DefaultContentFactory`, så borttagningsintervall bearbetas innan annonsinfogningar infogas.

   * `createCustomRangeOpportunities` har lagts till för att skapa alla affärsmöjligheter

      MARK - en affärsmöjlighet för varje giltigt markeringsintervall på `PlacementType.CUSTOM_RANGE` och `PlacementMode.MARK`

      DELETE - En möjlighet för varje giltigt borttagningsintervall på `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`

      REPLACE - Två möjligheter för varje giltigt ersättningsintervall:

      1. En möjlighet att ta bort intervall på `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`.

      1. En Primetime-annonsbeslutsmöjlighet på `PlacementType.MID_ROLL` eller `PlacementType.PRE_ROLL` och `PlacementMode.FREEREPLACE`

* `CustomRangeResolver` har lagts till:

   * `doCanResolve()` returnerar  `true` för borttagningsintervall.

   * `createDeleteRangeOperation()` har lagts till för att skapa `DeleteRange` för placeringen

* `CustomRangeHelper` har lagts till:

   * En vanlig verktygsklass som extraherar Mark/Delete/Replace `timeRanges` och bearbetar dem.
   * `extractCustomRangesMetadata()` har lagts till
   * `extractCustomRanges()` har lagts till
   * Tillagd `mergeRanges()` - löser konflikter och delmängder/sammanfogningar

* `MediaPlayerTimeline`:

   * &quot;>I `executeOperation()`, om åtgärden är `DeleteRange`, lade du till ett anrop för att ta bort metoden i åtgärden

   * I `executeOperation()`, om åtgärden är `NOPTimelineOperation` (tom `AdBreaks` kommer tillbaka från servern), lade till ett anrop för att rensa.

   * `onDeleteRangeComplete()` har lagts till
   * `removeRange()` har lagts till
   * I `adjustPlacement()`, för `PlacementMode.FREEREPLACE`-läget, nollställdes varaktigheten. Den här tidslängden behövs tidigare när du begär `AdBreaks`, och vid den här tidpunkten måste den vara noll för att infogas helt.

* `VideoEngineTimeline` Lagt till  `removeC3Ad()` - ring  `removeByLocalTime()` för borttagningsintervall

* `AdSignalingModeGenerator`

   * `doConfigure()` - Lös inte om ingen affärsmöjlighet genereras
   * `createInitialOpportunity()` - Generera ingen inledande affärsmöjlighet för  `AdSignalingMode.CUSTOM_RANGE`. `CustomRangeOpportunityGenerator` täcker detta redan.

* `DeleteRange`

   * Utökar `TimelineOperation`.
   * Skapad av `CustomRangeResolver` för borttagning och ersättning (borttagningsdelen av ersättning)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - tillåt paketering
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` Metoden  `accepts()` ändrades för att tillåta paketering av olika placeringstyp (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Felkorrigeringar som tillåter serveråsidosättning av annonsparametrar

* `AuditudeResolver` Metoden  `canBePacked()` ändrades för att tillåta packning

* `CustomAdResolver` Extraheringsfunktionerna  `timeRange` har tagits bort. Vi får en placering i taget och gör om den till `AdBreakPlacement timelineOperation`.

