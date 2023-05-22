---
description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
title: Krav för videospelare
exl-id: 23134e4c-6902-4b97-bf15-4524f47850e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Krav för videospelare {#video-player-requirements}

Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.

Om du vill använda API:t för annonsinfogning i Primetime måste en videospelare uppfylla följande:

* Kan spåra spelhuvudets position när innehållet spelas upp.
* Kan begära spårnings-URL:er vid angivna tidpunkter.
* Kan köras på en enhetsplattform som stöder HLS v3 eller senare, inklusive:

   * PTS-avbrott enligt `EXT-X-DISCONTINUITY` taggar
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Körs på en plattform som stöder HTTP-omdirigeringar och JSON-parsning.
* Webbaserade spelare måste köras på plattformar som stöder CORS.
