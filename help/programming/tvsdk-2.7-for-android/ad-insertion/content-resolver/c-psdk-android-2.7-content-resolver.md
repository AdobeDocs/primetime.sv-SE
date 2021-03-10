---
description: En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
title: Anpassa generatorer och innehållslösare för affärsmöjligheter
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Översikt {#customize-opportunity-generators-and-content-resolvers-overview}

En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

TVSDK innehåller följande standardgeneratorer för affärsmöjligheter:

* `ManifestCuesOpportunityGenerator` genererar affärsmöjligheter från standardannonsen (  `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genererar en inledande möjlighet för det angivna annonseringssigneringsläget. Detta ignorerar eventuell information om metadata eller tidsåtgång.
* `CustomMarkerOpportunityGenerator` skapar möjligheter att ersätta inbyggda C3-annonser.
* `AuditudeResolver`Möjlighetsgeneratorn skapar möjligheter när man är på med lata annonslösningar.

TVSDK innehåller även standardlösningar för innehåll:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, som kan kommunicera med Primetimes annonsbeslut.

Du kan åsidosätta standardgeneratorer för affärsmöjlighet och lösningar för innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Identifiera anpassade taggar för annonsinfogning
* Skapa en anpassad annonsleverantör.
* Svart ut innehåll.