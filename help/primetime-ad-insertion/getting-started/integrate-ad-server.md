---
title: Integrera er annonsserver
description: Integrera er annonsserver
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Integrera annonsservern {#integrate-ad-server}

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
