---
description: En affärsmöjlighetsdetektor är en TVADK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-description: En affärsmöjlighetsdetektor är en TVADK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
seo-title: Anpassa affärsmöjlighetsdetektorer och innehållslösningar
title: Anpassa affärsmöjlighetsdetektorer och innehållslösningar
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Översikt {#customize-opportunity-detectors-and-content-resolvers-overiew}

En affärsmöjlighetsdetektor är en TVADK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.

TVSDK innehåller standarddetektorer för affärsmöjligheter:

* `SpliceOutOpportunityDetector`, som förstår standard ad cues
* `AdSignalingModeOpportunityGenerator`, som skapar inledande annonsmöjligheter baserat på annonseringssigneringsläget
* `SpliceOutOpportunityGenerator`, som skapar annonsmöjligheter från valfri #EXT-X-CUE-tagg

TVSDK innehåller även en standardinnehållshanterare som tillhandahåller innehåll som ska infogas baserat på metadatanyckeln i spelarobjektet:

* `AuditudeResolver`, som kan kommunicera med Adobe Primetime annonsbeslutsservrar (tidigare Auditude) och returnera annonsbrytningar som ska placeras ut.

Du kan åsidosätta standardfunktioner för att identifiera affärsmöjligheter och tolka innehåll för att anpassa arbetsflödet för annonsering på följande sätt:

* Lägg till stöd för anpassad taggidentifiering
* Identifiera anpassade taggar för annonsinfogning
* Skapa en anpassad annonsleverantör
* Svart ut-innehåll

