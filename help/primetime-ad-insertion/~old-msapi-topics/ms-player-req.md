---
description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
title: Krav för videospelare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
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
* Körs på en plattform som stöder CORS.