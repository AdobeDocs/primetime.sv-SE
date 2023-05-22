---
title: Integrera er annonsserver
description: Integrera er annonsserver
exl-id: 4f2c75e0-db88-4c5d-8ddd-a5eab5d0b910
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Integrera er annonsserver {#integrate-ad-server}

Till att börja med får du en inloggning för att komma åt Primetimes Ad Insertion-konsol, där du ställer in regler som Primetime Ad Insertion använder för att vidarebefordra annonsförfrågningar till valfri annonsserver. Primetime Ad Insertion stöder de flesta VAST- eller VMAP-kompatibla annonsservrar.

>[!NOTE]
>
>[IAB VAST-sida](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Makrostöd {#macro-support}

Primetime Ad Insertion aktiverar följande annonseringsservermakron för alla strömmar:

* Cache-busting
* Programkontext eller sid-URL
* Tillgänglig varaktighet
* Aktuell videoresurs

Om du behöver ytterligare makron kontaktar du Adobe Primetime supportrepresentant.

## Avancerade funktioner {#advanced-features}

Primetime Ad Insertion har också regelbaserad beslutsprocess som möjliggör avancerade funktioner. Detta kan vara viktigt om du vill dirigera annonser till olika annonsservrar baserat på lagerrättigheter eller aktivera frekvensbegränsning för enskilda annonser. Mer information finns i [Avancerade funktioner](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
