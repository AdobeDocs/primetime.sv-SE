---
description: En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-description: En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-title: Anpassa generatorer och innehållslösare för affärsmöjligheter
title: Anpassa generatorer och innehållslösare för affärsmöjligheter
uuid: 97738b80-5cf8-494f-8811-449bceded220
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '249'
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