---
description: En affärsmöjlighetsdetektor är en TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-description: En affärsmöjlighetsdetektor är en TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-title: Generatorer för affärsmöjligheter och lösningar för innehåll
title: Generatorer för affärsmöjligheter och lösningar för innehåll
uuid: 593de6c0-042d-4a05-82d7-056a9a4500f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Generatorer för affärsmöjligheter och lösningar för innehåll {#opportunity-generators-and-content-resolvers}

En affärsmöjlighetsdetektor är en TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

TVSDK innehåller en standardannonsdetektor:

* `SpliceOutPlacementOpportunityDetector`, som förstår standard ad cues

TVSDK innehåller även standardinnehållslösningar som innehåller innehåll som ska infogas baserat på metadatanyckeln i spelarobjektet:

* `AuditudeResolver` för `AUDITUDE_METADATA_KEY`, som kan kommunicera med Adobe Primetime-annonsservrar (tidigare Auditude) och returnera annonsbrytningar som ska placeras.

* `MetadataResolver` for `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` for `TIME_RANGES_METADATA_KEY`

Du kan åsidosätta standardfunktioner för att identifiera affärsmöjligheter och tolka innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Lägg till stöd för anpassad taggidentifiering
* Identifiera anpassade taggar för annonsinfogning
* Skapa en anpassad annonsleverantör
* Svart ut-innehåll

TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.

En *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen, till exempel en utbrottsperiod. En *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) på tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats. Möjligheter identifieras i en tidslinje genom att en icke-standardtagg (icke-HLS) tas med.

När ditt program meddelas om en affärsmöjlighet (tagg) kan ditt program ändra tidslinjen genom att till exempel infoga en serie annonser, växla till en alternativ ström (utfall) eller på annat sätt redigera tidslinjeinnehållet. Som standard anropar TVSDK lämplig *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda TVSDK:s standardinnehållshanterare för annonser eller registrera en egen innehållshanterare.

Du kan också använda `MediaPlayerItemConfig.setAdTags` för att lägga till fler annonsmärkestaggar/tips så att TVSDK kan identifiera och använda `MediaPlayerItemConfig.subscribedTags` och meddela programmet om ytterligare taggar som kan ha annonsarbetsflödesinformation.

En möjlig användning för en anpassad lösare är för utbrottsperioder. För att kunna hantera dessa perioder kan programmet implementera och registrera en identifierare som hanterar svartout-taggar. När TVSDK påträffar den här taggen avsöks alla registrerade innehållslösningar för att hitta den första som hanterar den angivna taggen. I det här exemplet är det innehållslösaren för utsvärtning, som till exempel kan ersätta det aktuella objektet med alternativt innehåll i spelaren under den tid som anges av taggen.
