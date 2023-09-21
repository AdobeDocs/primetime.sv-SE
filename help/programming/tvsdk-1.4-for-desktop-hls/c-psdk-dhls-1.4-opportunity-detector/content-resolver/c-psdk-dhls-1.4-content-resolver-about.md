---
description: TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.
title: Generatorer för affärsmöjligheter och lösningar för innehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Generatorer för affärsmöjligheter och lösningar för innehåll{#opportunity-generators-and-content-resolvers}

TVSDK tillhandahåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser på tidslinjen, och dessa generatorer och lösare baseras på icke-standardiserade taggar i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet, till exempel indikatorer för en utbrottsperiod.

An *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen, till exempel en utbrottsperiod. An *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) på tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats. Affärsmöjligheter identifieras i en tidslinje i `TimedMetadata`. The `SpliceOutOpportunityGenerator` skapar möjligheter baserat på `TimedMetadata` objekt som skapas för varje annonstagg som har identifierats i manifestet, och `AdSignalingModeOpportunityGenerator` skapar den inledande affärsmöjligheten som baseras på `MediaPlayerItem` typ och tillhörande annonseringsläge.

När ditt program meddelas om en affärsmöjlighet (tagg) kan ditt program ändra tidslinjen genom att till exempel infoga en serie annonser, växla till en alternativ ström (utfall) eller på annat sätt redigera tidslinjeinnehållet. Som standard anropar TVSDK lämpliga *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda TVSDK:s standardinnehållshanterare för annonser eller registrera en egen innehållshanterare.

Du kan också använda `PSDKConfig.adTags` om du vill lägga till fler markörtaggar/tips för standardinställningen `SpliceOutOpportunityGenerator` klass och användning `PSDKConfig.setSubscribedTags` så att TVSDK kan meddela programmet om ytterligare taggar som kan ha information om annonsarbetsflöden.

En möjlig användning för en anpassad lösare är för utbrottsperioder. För att kunna hantera dessa perioder kan programmet implementera och registrera en identifierare som hanterar svartout-taggar. När TVSDK påträffar den här taggen avsöks alla registrerade innehållslösningar för att hitta den första som hanterar den angivna taggen. I det här exemplet är det innehållslösaren för utsvärtning, som till exempel kan ersätta det aktuella objektet med alternativt innehåll i spelaren under den tid som anges av taggen.
