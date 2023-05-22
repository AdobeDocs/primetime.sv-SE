---
description: Standardscenariot för den kreativa ompaketeringstjänsten (CRS) är att använda ett CDN (Content Delivery Network), men du kan distribuera CRS-resurser på mer än ett CDN.
title: Flera CDN-funktioner för CRS och leverans
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Flera CDN-funktioner för CRS och leverans {#multiple-cdn-support-for-crs-ad-delivery}

Standardscenariot för den kreativa ompaketeringstjänsten (CRS) är att använda ett CDN (Content Delivery Network), men du kan distribuera CRS-resurser på mer än ett CDN.

## Krav

Du kan använda flera CDN av följande skäl:

* Ett krav på att skala upp för stora visningshändelser
* Ett krav som matchar CDN-källan för CRS-resursen med CDN-källan för huvudinnehållet.
* Ett krav på att använda ett annat CDN än CRS-standard-CDN (Akamai).

När manifestservern gör en sökning efter omkodade begäranden, används en bootstrap-URL som innehåller ett antal frågeparametrar. Om du har konfigurerat en multi-CDN-miljö måste bootstrap-URL:en även innehålla `ptcdn` parameter. Manifestservern använder den här parametern för att identifiera CDN-servern som annonsens omkodade version ska hämtas från.

Mer information finns i [Stöd för flera CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) i CRS-dokumentationen.
