---
description: En affärsmöjlighetsdetektor är en TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
title: Generatorer för affärsmöjligheter och lösningar för innehåll
exl-id: 1f8e0baf-49ef-49a5-92d8-5eae31576974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Generatorer för affärsmöjligheter och lösningar för innehåll {#opportunity-generators-and-content-resolvers}

En affärsmöjlighetsdetektor är en TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

TVSDK innehåller en standardannonsdetektor:

* `PTOpportunityResolver`, som förstår standard ad cues

TVSDK innehåller även en standardinnehållshanterare som tillhandahåller innehåll som ska infogas baserat på metadatanyckeln i spelarobjektet:

* `PTContentResolver`

Du kan åsidosätta standardfunktioner för att identifiera affärsmöjligheter och tolka innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Lägg till stöd för anpassad taggidentifiering
* Identifiera anpassade taggar för annonsinfogning
* Skapa en anpassad annonsleverantör
* Svart ut-innehåll

<!--<a id="section_C2BA8F50230E4010ABFCD5D976BC1217"></a>-->

TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.

An *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen, till exempel en utbrottsperiod. An *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) på tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats. Affärsmöjligheter identifieras i en tidslinje i `PTTimedMetadata` genom att ta med en icke-standard-tagg (icke-HLS).

När ditt program meddelas om en affärsmöjlighet (tagg) kan ditt program ändra tidslinjen genom att till exempel infoga en serie annonser, växla till en alternativ ström (utfall) eller på annat sätt redigera tidslinjeinnehållet. Som standard anropar TVSDK lämpliga *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda TVSDK:s standardinnehållshanterare för annonser eller registrera en egen innehållshanterare.

Du kan också använda `PTSDKConfig.setAdTags` för att lägga till fler markörtaggar/tips så att TVSDK kan identifiera och använda `PTSDKConfig.setSubscribedTags` och meddela programmet om ytterligare taggar som kan innehålla information om annonsarbetsflöden.

En möjlig användning för en anpassad lösare är för utbrottsperioder. För att kunna hantera dessa perioder kan programmet implementera och registrera en identifierare som hanterar svartout-taggar. När TVSDK påträffar den här taggen avsöks alla registrerade innehållslösningar för att hitta den första som hanterar den angivna taggen. I det här exemplet är det innehållslösaren för utsvärtning, som till exempel kan ersätta det aktuella objektet med alternativt innehåll i spelaren under den tid som anges av taggen.
