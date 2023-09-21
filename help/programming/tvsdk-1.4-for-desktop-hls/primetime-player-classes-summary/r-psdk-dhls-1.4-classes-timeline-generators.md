---
description: Dessa klasser hjälper till att identifiera möjligheter i en tidslinje för placering av innehåll, som annonser.
title: Klasser för tidslinjegeneratorer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Klasser för tidslinjegeneratorer{#timeline-generators-classes}

Dessa klasser hjälper till att identifiera möjligheter i en tidslinje för placering av innehåll, som annonser.

Paket: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Namn | Beskrivning |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | En klass som skapar en inledande möjlighet för det angivna annonseringssigneringsläget. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Basklass för alla affärsmöjlighetsgeneratorer. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Gränssnitt som används av affärsmöjlighetsgeneratorer för att kommunicera med TVSDK-komponenter. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | En klass som övervakar uppspelningstidslinjen och identifierar annonsplaceringsmöjligheter som infogats i manifestet som SpliceOut-kommentarer. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Standardimplementering av en affärsmöjlighetsgenerator som använder tidsbestämd metadatainformation för att identifiera och generera annonsmöjligheter. |
