---
description: Dessa klasser hjälper till att identifiera möjligheter i en tidslinje för placering av innehåll, som annonser.
seo-description: Dessa klasser hjälper till att identifiera möjligheter i en tidslinje för placering av innehåll, som annonser.
seo-title: Klasser för generatorer för tidslinje
title: Klasser för generatorer för tidslinje
uuid: 1e36b738-0684-44f0-b3c3-dd656c70f705
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Klasser för generatorer för tidslinje{#timeline-generators-classes}

Dessa klasser hjälper till att identifiera möjligheter i en tidslinje för placering av innehåll, som annonser.

Paket: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html)

| Namn | Beskrivning |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html) | En klass som skapar en inledande möjlighet för det angivna annonseringssigneringsläget. |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html) | Basklass för alla affärsmöjlighetsgeneratorer. |
| [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html) | Gränssnitt som används av affärsmöjlighetsgeneratorer för att kommunicera med TVSDK-komponenter. |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html) | En klass som övervakar uppspelningstidslinjen och identifierar annonsplaceringsmöjligheter som infogats i manifestet som SpliceOut-kommentarer. |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html) | Standardimplementering av en affärsmöjlighetsgenerator som använder tidsbestämd metadatainformation för att identifiera och generera annonsmöjligheter. |