---
description: En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-description: En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-title: Anpassa generatorer för affärsmöjligheter och lösningar för innehåll
title: Anpassa generatorer för affärsmöjligheter och lösningar för innehåll
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Översikt {#customize-opportunity-generators-and-content-resolvers-overview}

En affärsmöjlighetsgenerator identifierar placeringsmöjligheter med anpassade taggar i en ström, anpassade markörer för annonseringsläge och så vidare. Affärsmöjlighetsgeneratorn skickar dessa placeringsmöjligheter till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

TVSDK innehåller följande standardgeneratorer för affärsmöjligheter:

* `ManifestCuesOpportunityGenerator` genererar affärsmöjligheter från standardannonsen ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genererar en inledande möjlighet för det angivna annonseringssigneringsläget. Detta ignorerar eventuell information om metadata eller tidsåtgång.
* `CustomMarkerOpportunityGenerator` skapar möjligheter att ersätta inbyggda C3-annonser.
* `AuditudeResolver`Möjlighetsgeneratorn skapar möjligheter när man är på med lata annonslösningar.

TVSDK innehåller även standardlösningar för innehåll:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, som kan kommunicera med Primetimes annonsbeslut.

Du kan åsidosätta standardgeneratorer för affärsmöjlighet och lösningar för innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Identifiera anpassade taggar för annonsinfogning. Mer information finns i [Anpassa generatorer för affärsmöjligheter och innehållslösningar](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Skapa en anpassad annonsleverantör.
* Svart ut innehåll.