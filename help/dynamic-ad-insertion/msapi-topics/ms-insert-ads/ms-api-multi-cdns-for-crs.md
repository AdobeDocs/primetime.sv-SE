---
description: Standardscenariot för den kreativa ompaketeringstjänsten (CRS) är att använda ett CDN (Content Delivery Network), men du kan distribuera CRS-resurser på mer än ett CDN.
seo-description: Standardscenariot för den kreativa ompaketeringstjänsten (CRS) är att använda ett CDN (Content Delivery Network), men du kan distribuera CRS-resurser på mer än ett CDN.
seo-title: Flera CDN-funktioner för CRS och leverans
title: Flera CDN-funktioner för CRS och leverans
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: f327b45de7e482dcb25407659846b2098f1fd49d

---


# Flera CDN-funktioner för CRS och leverans {#multiple-cdn-support-for-crs-ad-delivery}

Standardscenariot för den kreativa ompaketeringstjänsten (CRS) är att använda ett CDN (Content Delivery Network), men du kan distribuera CRS-resurser på mer än ett CDN.

## Krav

Du kan använda flera CDN av följande skäl:

* Ett krav på att skala upp för stora visningshändelser
* Ett krav som matchar CDN-källan för CRS-resursen med CDN-källan för huvudinnehållet.
* Ett krav på att använda ett annat CDN än CRS-standard-CDN (Akamai).

När manifestservern gör en sökning efter omkodade begäranden, används en bootstrap-URL som innehåller ett antal frågeparametrar. Om du har konfigurerat en multi-CDN-miljö måste bootstrap-URL:en även innehålla `ptcdn` parametern. Manifestservern använder den här parametern för att identifiera CDN-servern som annonsens omkodade version ska hämtas från.

Mer information finns i [Multi CDN-stöd](../../creative-repackaging-service/multi-cdn-supportt.md) i CRS-dokumentationen.
