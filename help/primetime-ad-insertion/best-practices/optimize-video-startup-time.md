---
title: Optimera starttiden för video
description: Optimera starttider för video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Optimera tidsöversikt för videostart {#optimize-video-start-up-times}

Primetime Ad Insertion har flera funktioner för att optimera starttiden för videofilmer, som cachelagring och regler för optimering av vägar/protokoll. Här följer några andra rekommendationer för att få snabbare videostart när du använder Primetime Ad Insertion:

* Hantera alla annonser och allt innehåll från CDN (Content Delivery Networks)

* Minska eller ta bort TLS-handskakningar mellan Primetime Ad Insertion och CDN:erna. Mer information finns i [Optimera vägar och protokoll](optimize-routes-protocols.md).

* Hantera annons- och innehållsfragment från samma CDN

* Infoga rubriker för cachekontroll för live-/VOD-innehåll och manifest

* Minska eller ta bort reklamleverantörer eller annonsskapare som inte svarar lika bra
