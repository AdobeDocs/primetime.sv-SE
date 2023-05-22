---
description: Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.
title: Ändringar i API:t för borttagning och ersättning av annonser
exl-id: bde8bd6e-0afe-42d0-b716-f33f75de757e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Ändringar i API:t för borttagning och ersättning av annonser{#ad-deletion-and-replacement-api-changes}

Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Nytt anpassat tidsintervall och signaleringsläge

* `AdvertisingMetadata` Nytt `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Anger tidsintervall för att markera, ta bort eller ersätta vid bearbetning av metadata

* `ContentResolver`

   * Nytt `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nytt `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nytt `ContentRemoval` class

   `TimelineOperation` klass som definierar det tidsintervall som ska tas bort från tidslinjen

* `AuditudeResolver`

   * Nytt `private LinkedList<AuditudeRequest> _requestQueue`
   * Nytt `void startConsumer()`: Startar bearbetningen av kön för anbudsförfrågningar för Primetime-annonsering och ser till att varje begäran utfärdas på `MIN_INIT_REQUEST_INTERVAL` intervall

   * Nytt `processReplacementRange()`: Extraherar tidsintervall från annonsens metadata och genererar `PlacementInformations`och skapar en Primetime-annonsbegäran som innehåller `PlacementInformations`.

   * Nytt `canDoResolver()`: Kontrollerar om placeringsmöjligheten har Primetime-annonsmetadata

* Nytt `CustomRangeHelper` Hjälpklass som extraherar tidsintervallmetadata från annonsmetadata och tar bort delmängder/överlappningar/ogiltiga tidsintervall.

* Nytt `DeleteContentResolver` Innehållslösare som åtgärdar placeringsmöjligheter för `PlacementInformation.Mode.DELETE`

* Nytt `NopTimelineOperation` Ny tidslinjeåtgärd för när ingen annonsradsplacering eller ersättning behöver göras. Den här klassen används för att skilja mellan detta och när ett fel inträffar under lösningsprocessen.

* `TimelineOperationQueue` Kontrollerar om tidslinjeåtgärden är en `NopTimelineOperation` före bearbetning.

* `CustomAdMarkersContentResolver` Nytt `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen `Mode.MARK`

* `MetadataResolver` Nytt `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen `Mode.INSERT`

* `DefaultMetadataKeys` Nytt `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nytt läge `enum (INSERT, DELETE, REPLACE, MARK)`
   * Ny typ `CUSTOM_TIME_RANGES`

* `TimeRange` Nytt `compareTo(TimeRange timeRange)`: Så kan sortera TimeRanges baserat på starttid

* Nytt `ReplacementTimeRange` Utökar `TimeRange` klass som representerar ett ersättningstidintervall, med `begin`, `end`och `replacement-duration` parameter.

* `TimeRangeCollection`

   * Nytt `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Bytt namn `CUSTOM_AD_MARKERS` till `MARK_RANGES`

   * Ändrad `toMetadata(Metadata options)` för att lägga in borttagnings-/markerings-/ersättningsintervall i annonsmetadata.

* `MediaPlayerNotification`

   * Nytt `UNDEFINED_TIME_RANGES`: När annonseringssignaleringsläget är Server Map eller Manifest Cues, och ersättningsintervall också finns i annonsens metadata, ignoreras ersättningsintervall.
   * Nytt `REPLACE_RANGES_NOT_AVAILABLE`: När signeringsläget Anpassade tidsintervall och ersättningsintervall inte är tillgängliga, skickas en varning.

* `AdvertisingFactory` Nytt `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nytt `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nytt `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * I `prepareToPlay()`: Gör en inledande sökning till 0, eftersom om-intervall `[0,n]` tas bort spelaren spelas inte upp automatiskt.

   * I `prepareToPlay()`: Går igenom listan med inledande placeringsinformation för `mediaplayerclient` att lösa.

   * I `extractAdSignalingMode()`: Anpassa för det nya läget Anpassat tidsintervall.
   * Nytt `private static List<PlacementInformation> createInitalPlacementInformations()`: Genererar inledande placeringsinformation för annonseringssigneringsläget och innehållslösningar (härledda från annonseringsmetadata).
   * I `ContentPlacementCompletedListener`: Kontrollerar om `mediaPlayerClient` är `doneInitialResolving` före samtal `endAdResolving`.

* `MediaPlayerClient`

   * Nytt `List<ContentResolver> _contentResolvers`
   * Nytt `int _reservations`
   * Nytt `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Söker efter vilken lösare som kan matcha `PlacementOpportunity`.

   * Ändrad kod för att skapa flera innehållslösningar.
   * Nytt `public boolean doneInitialResolving()`: Kontrollerar om det finns några möjligheter kvar att lösa.

* `VideoEngineTimeline`

   * Nytt `removeContent(TimelineOperation timelineOperation)`: Tar bort ett visst innehållsområde från tidslinjen.
   * Nytt `removeContentByLocalTime(long begin, long end)`: Tar bort innehåll efter lokal tid `begin` och `end`.

* `DefaultOpportunityDetectorFactory` Ändrad `createOpportunityDetector`: För VOD-strömmar returnerar du bara en ny `SpliceOutOpportunityDetector` om det inte finns några MARK- eller REPLACE-intervall (eftersom dessa intervall har prioritet framför signeringsläget).
