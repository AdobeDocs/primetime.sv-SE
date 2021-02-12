---
description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
seo-description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
seo-title: Krav för videospelare
title: Krav för videospelare
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Krav för videospelaren {#video-player-requirements}

Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.

Om du vill använda API:t för annonsinfogning i Primetime måste en videospelare uppfylla följande:

* Kan spåra spelhuvudets position när innehållet spelas upp.
* Kan begära spårnings-URL:er vid angivna tidpunkter.
* Kan köras på en enhetsplattform som stöder HLS v3 eller senare, inklusive:

   * PTS-avbrott markerade med `EXT-X-DISCONTINUITY`-taggar
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Körs på en plattform som stöder HTTP-omdirigeringar och JSON-parsning.
* Webbaserade spelare måste köras på plattformar som stöder CORS.