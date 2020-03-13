---
description: Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.
seo-description: Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.
seo-title: Ändringar i API:t för borttagning och ersättning av annonser
title: Ändringar i API:t för borttagning och ersättning av annonser
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ändringar i API:t för borttagning och ersättning av annonser{#ad-deletion-and-replacement-api-changes}

Dessa ändringar i Android TVSDK API har stöd för att ta bort och ersätta annonser.

* `AdSignalingMode` Nytt anpassat tidsintervall och signaleringsläge

* `AdvertisingMetadata` Nytt `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Anger tidsintervall för att markera, ta bort eller ersätta vid bearbetning av metadata

* `ContentResolver`

   * Nytt `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nytt `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Ny `ContentRemoval` klass

   `TimelineOperation` klass som definierar det tidsintervall som ska tas bort från tidslinjen

* `AuditudeResolver`

   * Nytt `private LinkedList<AuditudeRequest> _requestQueue`
   * Nytt `void startConsumer()`: Startar bearbetningen av kön för anbudsförfrågningar för Primetime-annonsering och ser till att varje begäran skickas med `MIN_INIT_REQUEST_INTERVAL` intervaller

   * Nytt `processReplacementRange()`: Extraherar tidsintervall från annonsmetadata och genererar `PlacementInformations`och skapar en Primetime-annonsbegäran som innehåller `PlacementInformations`.

   * Nytt `canDoResolver()`: Kontrollerar om placeringsmöjligheten har Primetime-annonsmetadata

* Ny `CustomRangeHelper` Helper-klass som extraherar metadata för tidsintervall från annonsmetadata och tar bort delmängder/överlappningar/ogiltiga tidsintervall.

* Ny `DeleteContentResolver` innehållslösare som åtgärdar placeringsmöjligheter i `PlacementInformation.Mode.DELETE`

* Ny `NopTimelineOperation` ny tidslinjeåtgärd för när ingen annonsradsplacering eller ersättning behöver göras. Den här klassen används för att skilja mellan detta och när ett fel inträffar under lösningsprocessen.

* `TimelineOperationQueue` Kontrollerar om tidslinjeåtgärden är en åtgärd `NopTimelineOperation` före bearbetning.

* `CustomAdMarkersContentResolver` Nytt `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen `Mode.MARK`

* `MetadataResolver` Nytt `canDoResolve()`: Kontrollerar om en placeringsmöjlighet är av typen `Mode.INSERT`

* `DefaultMetadataKeys` Nytt `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nytt läge `enum (INSERT, DELETE, REPLACE, MARK)`
   * Ny typ `CUSTOM_TIME_RANGES`

* `TimeRange` Nytt `compareTo(TimeRange timeRange)`: Så kan sortera TimeRanges baserat på starttid

* Nytt `ReplacementTimeRange` Utökar den `TimeRange` klass som representerar ett nytt tidsintervall, med en `begin`parameter, `end`och en `replacement-duration` parameter.

* `TimeRangeCollection`

   * Nytt `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Bytt namn `CUSTOM_AD_MARKERS` till `MARK_RANGES`

   * Ändrad `toMetadata(Metadata options)` för att lägga in intervall för borttagning/markering/ersättning i annonsmetadata.

* `MediaPlayerNotification`

   * Nytt `UNDEFINED_TIME_RANGES`: När annonseringssignaleringsläget är Server Map eller Manifest Cues, och ersättningsintervall också finns i annonsens metadata, ignoreras ersättningsintervall.
   * Nytt `REPLACE_RANGES_NOT_AVAILABLE`: När signeringsläget Anpassade tidsintervall och ersättningsintervall inte är tillgängliga, skickas en varning.

* `AdvertisingFactory` Nytt `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nytt `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nytt `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * I `prepareToPlay()`: Gör en inledande sökning till 0, eftersom mediespelaren inte spelas upp automatiskt om intervallet `[0,n]` tas bort.

   * I `prepareToPlay()`: Går igenom listan med inledande placeringsinformation som ska `mediaplayerclient` åtgärdas.

   * I `extractAdSignalingMode()`: Anpassa för det nya läget Anpassat tidsintervall.
   * Nytt `private static List<PlacementInformation> createInitalPlacementInformations()`: Genererar inledande placeringsinformation för annonseringssigneringsläget och innehållslösningar (härledda från annonseringsmetadata).
   * I `ContentPlacementCompletedListener`: Kontrollerar om `mediaPlayerClient` är `doneInitialResolving` före anrop `endAdResolving`.

* `MediaPlayerClient`

   * Nytt `List<ContentResolver> _contentResolvers`
   * Nytt `int _reservations`
   * Nytt `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Söker efter vilken lösare som kan matcha `PlacementOpportunity`.

   * Ändrad kod för att skapa flera innehållslösningar.
   * Nytt `public boolean doneInitialResolving()`: Kontrollerar om det finns några möjligheter kvar att lösa.

* `VideoEngineTimeline`

   * Nytt `removeContent(TimelineOperation timelineOperation)`: Tar bort ett visst innehållsområde från tidslinjen.
   * Nytt `removeContentByLocalTime(long begin, long end)`: Tar bort innehåll efter lokal tid angiven `begin` och `end`.

* `DefaultOpportunityDetectorFactory` Ändrad `createOpportunityDetector`: För VOD-strömmar returnerar du bara ett nytt `SpliceOutOpportunityDetector` om det inte finns något MARK- eller REPLACE-intervall (eftersom dessa intervall har prioritet framför signeringsläget).

