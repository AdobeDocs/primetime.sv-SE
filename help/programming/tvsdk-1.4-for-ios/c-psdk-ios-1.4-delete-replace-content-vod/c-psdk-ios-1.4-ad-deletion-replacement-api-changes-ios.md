---
description: Följande ändringar i TVSDK har stöd för att ta bort och ersätta annonser.
seo-description: Följande ändringar i TVSDK har stöd för att ta bort och ersätta annonser.
seo-title: Ändringar i API:t för borttagning och ersättning av annonser
title: Ändringar i API:t för borttagning och ersättning av annonser
uuid: 7cc50e7a-666f-4588-9c16-ad6d7d75cb65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ändringar i API:t för borttagning och ersättning av annonser{#ad-deletion-and-replacement-api-changes}

Följande ändringar i TVSDK har stöd för att ta bort och ersätta annonser.

**Nya API:er**

* `PTTimeRangeCollection` är en public-klass som definierar en fördefinierad uppsättning intervall och en typ:

   * `property PTTimeRangeCollectionType type` anger typen av tidsintervall.
   * `property NSArray* ranges` används för att ange tidsintervall.

      Den förväntade typen av objekt i arrayen är `PTReplacementTimeRange` eller `CMTimeRange`.

      >[!TIP]
      >
      >Alla objekt i arrayen måste vara av samma typ.

   * `PTTimeRangeCollectionType` är en uppräkning som definierar beteendet för de intervall som definieras i `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: Intervalltypen är *Mark*. Intervallen används för att markera intervallen i innehållet som annonser.

      * `PTTimeRangeCollectionTypeDeleteRanges`: Intervalltypen är Delete. De definierade intervallen tas bort från huvudinnehållet innan annonsinfogningen.
      * `PTTimeRangeCollectionTypeReplaceRanges`: Intervalltypen är Ersätt. De definierade intervallen ersätts från huvudområdet med annonser (annonseringsläget är inställt på `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Ny offentlig klass som definierar ett enskilt intervall av `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Definierar intervallets start och varaktighet.
   * `property long replacementDuration` - Om typen av `TimeRangeCollection` är `PTTimeRangeCollectionTypeReplaceRanges`, `replacementDuration` används den för att skapa en placeringsmöjlighet (annonsinfogning) med en varaktighet på `replacementDuration`. Om inställningen inte `replacementDuration` är aktiverad avgör annonsservern hur länge och hur många annonser som gäller för placeringsmöjligheten.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - En ny typ av `PTAdSignalingMode`. Det här läget används tillsammans med typen `PTTimeRangeCollection` med `PTTimeRangeCollectionReplace` för annonsinfogning baserat på ersättningsintervallen.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - För inställning av tidsintervall som används i intervallen för markering/borttagning/ersättning i uppspelningsinnehållet.

* Varningsloggar:

   * `UNDEFINED_TIME_RANGES`

      * Typ - Varning
      * Beskrivning - Annonssignaleringsläget definieras som anpassade intervall, men de anpassade intervallen definieras inte.
   * `INVALID_TIME_RANGES`

      * Typ - Varning
      * Beskrivning - Ett eller flera tidsintervall är ogiltiga och ignoreras eller ändras.


**Föråldrade API:er**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Den här egenskapen användes tidigare för att definiera C3-intervall för märkning. Den är nu föråldrad eftersom dessa intervall anges via `PTTimeRangeCollection`.

