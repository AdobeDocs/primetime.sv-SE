---
description: Webbläsarens TVSDK innehåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser i tidslinjen, och dessa generatorer och lösare är baserade på taggar som inte är standard i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet.
seo-description: Webbläsarens TVSDK innehåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser i tidslinjen, och dessa generatorer och lösare är baserade på taggar som inte är standard i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet.
seo-title: Generatorer för affärsmöjligheter och lösningar för innehåll
title: Generatorer för affärsmöjligheter och lösningar för innehåll
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Generatorer och innehållslösningar för affärsmöjligheter{#opportunity-generators-and-content-resolvers}

Webbläsarens TVSDK innehåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser i tidslinjen, och dessa generatorer och lösare är baserade på taggar som inte är standard i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet.

En *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen. En *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) i tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats.

Affärsmöjligheter identifieras i en tidslinje i `TimedMetata`. `ManifestCuesOpportunityGenerator` skapar möjligheter baserat på de `TimedMetadata`-objekt som skapas för varje annonstagg (i `MediaPlayerItemConfig.adTags`) som har identifierats i manifestet. `AdSignalingModeOpportunityGenerator` skapar den inledande affärsmöjligheten som baseras på typen `MediaPlayerItem` och dess associerade annonseringsläge.

>[!TIP]
>
>Om egenskapen `AdvertisingMetadata.livePreroll` eller `AdvertisingMetadata.preroll` är inställd genererar `AdSignalingModeOpportunityGenerator` en pre-roll-möjlighet för liveströmmar.

När ditt program meddelas om en affärsmöjlighet (tagg) kan programmet ändra tidslinjen genom att till exempel infoga en serie annonser. Som standard anropar Browser TVSDK rätt *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda webbläsarens TVSDK-annonsinnehållshanterare eller registrera en egen innehållshanterare.

Du kan också använda `MediaPlayerItemConfig.adTags` för att lägga till fler annonsmärkestaggar/tips för standardklassen `ManifestCuesOpportunityGenerator` och använda `MediaPlayerItemConfig.subscribedTags` så att TVSDK kan meddela programmet om ytterligare taggar som kan ha annonsarbetsflödesinformation.

>[!TIP]
>
>Standardvärdena för `MediaPlayerItemConfig.adTags` och `MediaPlayerItemConfig.subscribeTags` är `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

