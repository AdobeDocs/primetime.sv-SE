---
description: Följande ändringar i TVSDK har stöd för att ta bort och ersätta annonser.
title: Ändringar i API:t för borttagning och ersättning av annonser
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

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
   * `property long replacementDuration` - Om typen av `TimeRangeCollection` är `PTTimeRangeCollectionTypeReplaceRanges`, `replacementDuration` används för att skapa en platsmöjlighet (annonsinfogning) med en varaktighet på `replacementDuration`. Om `replacementDuration` är inte inställt, kommer annonsservern att bestämma längden och antalet annonser för den placeringsmöjligheten.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - En ny typ av `PTAdSignalingMode`. Det här läget används tillsammans med `PTTimeRangeCollection` med text `PTTimeRangeCollectionReplace` för annonsinfogning baserat på ersättningsintervall.

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

