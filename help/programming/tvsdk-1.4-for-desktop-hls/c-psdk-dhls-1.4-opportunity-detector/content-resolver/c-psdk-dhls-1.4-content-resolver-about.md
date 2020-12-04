---
description: TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.
seo-description: TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.
seo-title: Generatorer för affärsmöjligheter och lösningar för innehåll
title: Generatorer för affärsmöjligheter och lösningar för innehåll
uuid: 9eaeeacf-9e7c-4ebb-a91e-fbc53e96d2c3
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Generatorer och innehållslösningar för affärsmöjligheter{#opportunity-generators-and-content-resolvers}

TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.

En *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen, till exempel en utbrottsperiod. En *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) i tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats. Affärsmöjligheter identifieras i en tidslinje i `TimedMetadata`. `SpliceOutOpportunityGenerator` skapar affärsmöjligheter baserat på de `TimedMetadata`-objekt som skapas för varje annonstagg som har identifierats i manifestet, och `AdSignalingModeOpportunityGenerator` skapar den inledande affärsmöjligheten som baseras på typen `MediaPlayerItem` och dess associerade annonseringsläge.

När ditt program meddelas om en affärsmöjlighet (tagg) kan ditt program ändra tidslinjen genom att till exempel infoga en serie annonser, växla till en alternativ ström (utfall) eller på annat sätt redigera tidslinjeinnehållet. Som standard anropar TVSDK rätt *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda TVSDK:s standardinnehållshanterare för annonser eller registrera en egen innehållshanterare.

Du kan också använda `PSDKConfig.adTags` för att lägga till fler annonsmärkestaggar/tips för standardklassen `SpliceOutOpportunityGenerator` och använda `PSDKConfig.setSubscribedTags` så att TVSDK kan meddela programmet om ytterligare taggar som kan ha annonsarbetsflödesinformation.

En möjlig användning för en anpassad lösare är för utbrottsperioder. För att kunna hantera dessa perioder kan programmet implementera och registrera en identifierare som hanterar svartout-taggar. När TVSDK påträffar den här taggen avsöks alla registrerade innehållslösningar för att hitta den första som hanterar den angivna taggen. I det här exemplet är det innehållslösaren för utsvärtning, som till exempel kan ersätta det aktuella objektet med alternativt innehåll i spelaren under den tid som anges av taggen.
