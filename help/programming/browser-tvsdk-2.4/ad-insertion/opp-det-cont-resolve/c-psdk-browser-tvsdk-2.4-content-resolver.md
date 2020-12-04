---
description: En affärsmöjlighetsdetektor är en Browser TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-description: En affärsmöjlighetsdetektor är en Browser TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-title: Anpassa affärsmöjlighetsdetektorer och innehållslösningar
title: Anpassa affärsmöjlighetsdetektorer och innehållslösningar
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Översikt {#customize-opportunity-detectors-and-content-resolvers-overview}

En affärsmöjlighetsdetektor är en Browser TVSDK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

Webbläsarens TVSDK innehåller följande standarddetektorer för affärsmöjligheter:

* `AdSignalingModeOpportunityGenerator`, som skapar inledande annonsmöjligheter baserat på annonseringssigneringsläget.
* `ManifestCuesOpportunityGenerator`, vilket skapar möjligheter till annonsplacering från alla splice-out-taggar.

Webbläsarens TVSDK innehåller även standardinnehållslösare, till exempel `AuditudeResolver`, som innehåller innehåll som infogas baserat på metadatanyckeln i spelarobjektet. `AuditudeResolver` kan kommunicera med Adobe Primetime annonsservrar och returnera annonsbrytningar som ska placeras ut.

Du kan åsidosätta standardfunktioner för att identifiera affärsmöjligheter och tolka innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Lägg till stöd för anpassad taggidentifiering
* Identifiera anpassade taggar för annonsinfogning
* Skapa en anpassad annonsleverantör

