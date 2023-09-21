---
description: Webbläsarens TVSDK innehåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser i tidslinjen, och dessa generatorer och lösare är baserade på taggar som inte är standard i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet.
title: Generatorer för affärsmöjligheter och lösningar för innehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Generatorer för affärsmöjligheter och lösningar för innehåll{#opportunity-generators-and-content-resolvers}

Webbläsarens TVSDK innehåller standardgeneratorer för affärsmöjligheter och innehållslösningar som placerar annonser i tidslinjen, och dessa generatorer och lösare är baserade på taggar som inte är standard i manifestet. Programmet kan behöva ändra tidslinjen baserat på de möjligheter som identifieras i manifestet.

An *`opportunity`* representerar en intressepunkt på tidslinjen som vanligtvis anger en annonsmöjlighet. Den här affärsmöjligheten kan även indikera en anpassad åtgärd som kan påverka tidslinjen. An *`opportunity generator`* identifierar specifika affärsmöjligheter (taggar) på tidslinjen och meddelar TVSDK om att dessa affärsmöjligheter har taggats.

Affärsmöjligheter identifieras i en tidslinje i `TimedMetata`. The `ManifestCuesOpportunityGenerator` skapar möjligheter baserat på `TimedMetadata` objekt som skapas för varje delningstagg (in `MediaPlayerItemConfig.adTags`) som har identifierats i manifestet. The `AdSignalingModeOpportunityGenerator` skapar den inledande affärsmöjligheten som baseras på `MediaPlayerItem` typ och tillhörande annonseringsläge.

>[!TIP]
>
>Om `AdvertisingMetadata.livePreroll` eller `AdvertisingMetadata.preroll` egenskapen är inställd, `AdSignalingModeOpportunityGenerator` genererar en pre-roll-möjlighet för liveströmmar.

När ditt program meddelas om en affärsmöjlighet (tagg) kan programmet ändra tidslinjen genom att till exempel infoga en serie annonser. Som standard anropar webbläsarens TVSDK rätt *`content resolver`* för att implementera de ändringar eller åtgärder som krävs på tidslinjen. Ditt program kan använda webbläsarens TVSDK-annonsinnehållshanterare som standard eller registrera en egen innehållshanterare.

Du kan också använda `MediaPlayerItemConfig.adTags` om du vill lägga till fler markörtaggar/tips för standardinställningen `ManifestCuesOpportunityGenerator` klass och användning `MediaPlayerItemConfig.subscribedTags` så att TVSDK kan meddela programmet om ytterligare taggar som kan ha information om annonsarbetsflöde.

>[!TIP]
>
>Standardvärdena för `MediaPlayerItemConfig.adTags` och `MediaPlayerItemConfig.subscribeTags` är `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
