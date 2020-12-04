---
description: Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.
seo-description: Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.
seo-title: Ändringar i API:t för borttagning och ersättning av annonser
title: Ändringar i API:t för borttagning och ersättning av annonser
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Ändringar i API:t för borttagning och ersättning av annonser{#ad-deletion-and-replacement-api-changes}

Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Nytt anpassat tidsintervall och signaleringsläge

* `AdvertisingMetadata` Nytt  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Anger tidsintervall för att markera, ta bort eller ersätta vid bearbetning av metadata

* `ContentResolver`

   * Ny `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Ny `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Ny `ContentRemoval`-klass

   `TimelineOperation` klass som definierar det tidsintervall som ska tas bort från tidslinjen

* `AuditudeResolver`

   * Ny `private LinkedList<AuditudeRequest> _requestQueue`
   * Ny `void startConsumer()`: Startar bearbetningen av kön för Primetime-annonsbegäranden och ser till att varje begäran utfärdas med `MIN_INIT_REQUEST_INTERVAL` intervall

   * Ny `processReplacementRange()`: Extraherar tidsintervall från annonsmetadata och genererar `PlacementInformations` och skapar en Primetime-annonsbeslutsbegäran som innehåller `PlacementInformations`.

   * Ny `canDoResolver()`: Kontrollerar om placeringsmöjligheten har Primetime-annonsmetadata

* Den nya klassen `CustomRangeHelper` Helper som extraherar tidsintervallmetadata från annonsmetadata och tar bort delmängder/överlappningar/ogiltiga tidsintervall.

* Ny `DeleteContentResolver` Content resolver som löser placeringsmöjligheterna i `PlacementInformation.Mode.DELETE`

* Ny `NopTimelineOperation` ny tidslinjeåtgärd för när ingen annonsradsplacering eller ersättning behöver göras. Den här klassen används för att skilja mellan detta och när ett fel inträffar under lösningsprocessen.

* `TimelineOperationQueue` Kontrollerar om tidslinjeåtgärden är en åtgärd  `NopTimelineOperation` före bearbetning.

* `CustomAdMarkersContentResolver` Nytt  `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen  `Mode.MARK`

* `MetadataResolver` Nytt  `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen  `Mode.INSERT`

* `DefaultMetadataKeys` Nytt  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nytt läge `enum (INSERT, DELETE, REPLACE, MARK)`
   * Ny typ `CUSTOM_TIME_RANGES`

* `TimeRange` Nytt  `compareTo(TimeRange timeRange)`: Så kan sortera TimeRanges baserat på starttid

* Ny `ReplacementTimeRange` Utökar klassen `TimeRange` som representerar en ersättningstid, med en `begin`-, `end`- och `replacement-duration`-parameter.

* `TimeRangeCollection`

   * Ny `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Namnet på `CUSTOM_AD_MARKERS` har ändrats till `MARK_RANGES`

   * Ändrad `toMetadata(Metadata options)` för att lägga in borttagnings-/märkesintervall i annonsmetadata.

* `MediaPlayerNotification`

   * Ny `UNDEFINED_TIME_RANGES`: När annonseringssignaleringsläget är Server Map eller Manifest Cues, och ersättningsintervall också finns i annonsens metadata, ignoreras ersättningsintervall.
   * Ny `REPLACE_RANGES_NOT_AVAILABLE`: När signeringsläget Anpassade tidsintervall och ersättningsintervall inte är tillgängliga, skickas en varning.

* `AdvertisingFactory` Nytt  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nytt  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nytt  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * I `prepareToPlay()`: Gör en inledande sökning till 0, eftersom mediespelaren inte spelas upp automatiskt om intervallet `[0,n]` tas bort.

   * I `prepareToPlay()`: Går igenom listan med inledande placeringsinformation som `mediaplayerclient` ska matchas.

   * I `extractAdSignalingMode()`: Anpassa för det nya läget Anpassat tidsintervall.
   * Ny `private static List<PlacementInformation> createInitalPlacementInformations()`: Genererar inledande placeringsinformation för annonseringssigneringsläget och innehållslösningar (härledda från annonseringsmetadata).
   * I `ContentPlacementCompletedListener`: Kontrollerar om `mediaPlayerClient` är `doneInitialResolving` innan `endAdResolving` anropas.

* `MediaPlayerClient`

   * Ny `List<ContentResolver> _contentResolvers`
   * Ny `int _reservations`
   * Ny `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Söker efter vilken matchare som kan matcha `PlacementOpportunity`.

   * Ändrad kod för att skapa flera innehållslösningar.
   * Ny `public boolean doneInitialResolving()`: Kontrollerar om det finns några möjligheter kvar att lösa.

* `VideoEngineTimeline`

   * Ny `removeContent(TimelineOperation timelineOperation)`: Tar bort ett visst innehållsområde från tidslinjen.
   * Ny `removeContentByLocalTime(long begin, long end)`: Tar bort innehåll med lokal tid angiven `begin` och `end`.

* `DefaultOpportunityDetectorFactory` Ändrad  `createOpportunityDetector`: För VOD-strömmar returnerar du bara ett nytt  `SpliceOutOpportunityDetector` om det inte finns något MARK- eller REPLACE-intervall (eftersom dessa intervall har prioritet framför signeringsläget).

