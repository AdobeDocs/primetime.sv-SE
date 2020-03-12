---
description: De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.
seo-description: De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.
seo-title: Ändringar i API:t för borttagning och ersättning av annonser
title: Ändringar i API:t för borttagning och ersättning av annonser
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Ändringar i API:t för borttagning och ersättning av annonser {#ad-deletion-and-replacement-api-changes}

De här ändringarna i TVSDK har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Signeringsläge har lagts till `CUSTOM_RANGES` .

* `OpportunityGenerator`  `extractAdSignalingMode()` - Ange `AdSignalingMode.CUSTOM_RANGES` om ersättningsintervall finns i metadata.

* `PlacementType` Tillagd `CUSTOM_RANGE` typ.

* `PlacementMode`

   * Läget har lagts till `DELETE` .
   * Tillagt `MARK` läge
   * Läget har lagts till - Det här läget har en varaktighet men är en ren infogning `FreeReplace`

* `TimeRange` Inte längre en `final` klass

* Tillagd `ReplaceTimeRange()` metod

   Utökar `TimeRange` till att ha en `replacementDuration` egenskap. För MARK- och DELETE-fallen `replacementDuration` är 0.

* `TimeRangeCollection`

   * Verktygsfunktion har lagts till för att extrahera `toReplaceMetadata()` `timeRanges`.

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
      * Flyttad `CustomAdMarkerResolver` före `AuditudeResolver`


* Tillagd `CustomRangeOpportunityGenerator`

   * `doUpdate()` Leaves empty - no Update, VOD
   * `doProcess()` Skapar en ny placering av en ny typ `Placement.Delete_Range`

   * Tillagd högst upp i generatorlistan i `CustomRangeOppotunityGenerator` `DefaultContentFactory`så radera intervall bearbetas före annonsinfogningar.

   * Lagt `createCustomRangeOpportunities` till för att skapa alla affärsmöjligheter

      MARK - en affärsmöjlighet för varje giltigt markeringsintervall för `PlacementType.CUSTOM_RANGE` och `PlacementMode.MARK`

      DELETE - En affärsmöjlighet för varje giltigt borttagningsintervall för `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`

      REPLACE - Två möjligheter för varje giltigt ersättningsintervall:

      1. En möjlighet att ta bort intervall för `PlacementType.CUSTOM_RANGE` och `PlacementMode.DELETE`.

      1. Primetimes annonsbeslut och möjlighet till `PlacementType.MID_ROLL` eller `PlacementType.PRE_ROLL` och `PlacementMode.FREEREPLACE`

* Tillagt `CustomRangeResolver`:

   * `doCanResolve()` returnerar `true` för borttagningsintervall.

   * Tillagd `createDeleteRangeOperation()` för att skapa `DeleteRange` för placeringen

* Tillagt `CustomRangeHelper`:

   * En vanlig verktygsklass som extraherar Mark/Delete/Replace `timeRanges` och bearbetar dem.
   * Tillagd `extractCustomRangesMetadata()`
   * Tillagd `extractCustomRanges()`
   * Tillagd `mergeRanges()` - Löser konflikter och delmängder/sammanfogningar

* `MediaPlayerTimeline`:

   * &quot;>I `executeOperation()`, om åtgärden är `DeleteRange`, läggs ett anrop till metoden remove till i åtgärden

   * I `executeOperation()`läggs ett anrop till för att rensa om åtgärden är `NOPTimelineOperation` (tom `AdBreaks` kommer tillbaka från servern).

   * Tillagd `onDeleteRangeComplete()`
   * Tillagd `removeRange()`
   * I `adjustPlacement()``PlacementMode.FREEREPLACE` läget nollställdes längden. Den här tidslängden behövs tidigare vid begäran `AdBreaks`och vid den här tidpunkten måste den vara noll för att infogas helt.

* `VideoEngineTimeline` Tillagt `removeC3Ad()` - ring `removeByLocalTime()` för borttagningsintervall

* `AdSignalingModeGenerator`

   * `doConfigure()` - Lös inte om ingen affärsmöjlighet genereras
   * `createInitialOpportunity()` - Generera ingen inledande affärsmöjlighet för `AdSignalingMode.CUSTOM_RANGE`. Det `CustomRangeOpportunityGenerator` täcker redan detta.

* `DeleteRange`

   * Utökar `TimelineOperation`.
   * Skapad av `CustomRangeResolver` för borttagning och ersättning (borttagningsdelen av ersättning)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - tillåt paketering
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` Metoden har ändrats så att den tillåter paketering av olika placeringstyp (pre-roll, mid-roll, post-roll) `accepts()`

* `AuditudeRequestHelper` Felkorrigeringar som tillåter serveråsidosättning av annonsparametrar

* `AuditudeResolver` Metoden har `canBePacked()` ändrats så att den tillåter packning

* `CustomAdResolver` Extraheringsfunktionerna har tagits bort `timeRange` . Vi får en placering i taget och förvandlar det till en `AdBreakPlacement timelineOperation`.

