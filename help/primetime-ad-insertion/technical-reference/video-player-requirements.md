---
description: Alla videospelare måste tillhandahålla funktioner som manifestservern använder för att infoga annonser och aktivera annonsspårning.
title: Krav för videospelare
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Krav för videospelare {#video-player-requirements}

Alla videospelare måste tillhandahålla funktioner som manifestservern använder för att infoga annonser och aktivera annonsspårning.

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
