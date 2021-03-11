---
description: TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.
title: Generatorer för affärsmöjligheter och lösningar för innehåll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Generatorer och innehållslösningar för affärsmöjligheter {#opportunity-generators-and-content-resolvers}

TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.

En *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen, till exempel en utbrottsperiod. En *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) i tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats. Möjligheter identifieras i en tidslinje genom att en icke-standardtagg (icke-HLS) tas med.

När ditt program meddelas om en möjlighet kan programmet ändra tidslinjen genom att infoga en serie annonser, växla till en alternativ ström (utfall) eller på annat sätt redigera tidslinjeinnehållet. Som standard anropar TVSDK rätt *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda TVSDK:s standardinnehållshanterare för annonser eller registrera en egen innehållshanterare.

Du kan också använda `MediaPlayerItemConfig.setAdTags` för att lägga till fler annonsmärkestaggar/tips så att TVSDK kan identifiera och använda `MediaPlayerItemConfig.subscribedTags` och meddela programmet om ytterligare taggar som kan ha annonsarbetsflödesinformation.

En möjlig användning för en anpassad lösare är för utbrottsperioder. För att kunna hantera dessa perioder kan programmet implementera och registrera en identifierare som hanterar svartout-taggar. När TVSDK påträffar den här taggen avsöks alla registrerade innehållslösningar för att hitta den första som hanterar den angivna taggen. I det här exemplet är det innehållslösaren för utsvärtning, som till exempel kan ersätta det aktuella objektet med alternativt innehåll i spelaren under den tid som anges av taggen.
