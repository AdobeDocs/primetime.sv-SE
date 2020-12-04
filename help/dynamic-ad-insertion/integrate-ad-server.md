---
title: Integrera er annonsserver
description: Integrera er annonsserver
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '141'
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

<!--For technical information regarding specific ad servers or ad macros, see [Supported ad servers and macros](supported-ad-servers-and-macros.md).-->

Om du behöver ytterligare makron kontaktar du Adobe Primetime supportrepresentant.

## Avancerade funktioner {#advanced-features}

Primetime Ad Insertion har också regelbaserad beslutsprocess som möjliggör avancerade funktioner. Detta kan vara viktigt om du vill dirigera annonser till olika annonsservrar baserat på lagerrättigheter eller aktivera frekvensbegränsning för enskilda annonser. <!--For more information, see [Advanced Features](route-ads-based-on-rules.md).-->
