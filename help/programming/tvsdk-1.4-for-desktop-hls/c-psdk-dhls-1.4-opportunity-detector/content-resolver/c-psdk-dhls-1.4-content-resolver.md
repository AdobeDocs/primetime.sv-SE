---
description: En affärsmöjlighetsdetektor är en TVADK-komponent som identifierar anpassade taggar i en ström och identifierar placeringsmöjligheter. Dessa möjligheter skickas till innehållslösaren, som anpassar arbetsflödet för infogning av innehåll/annonser baserat på placeringsmöjlighetens egenskaper och metadata.
title: Anpassa affärsmöjlighetsdetektorer och innehållslösningar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
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

