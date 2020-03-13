---
description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
seo-description: Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.
seo-title: Krav för videospelare
title: Krav för videospelare
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Krav för videospelare {#video-player-requirements}

Alla videospelare måste tillhandahålla funktioner som manifestservern förlitar sig på för att infoga annonser och aktivera annonsspårning.

Om du vill använda API:t för annonsinfogning i Primetime måste en videospelare uppfylla följande:

* Kan spåra spelhuvudets position när innehållet spelas upp.
* Kan begära spårnings-URL:er vid angivna tidpunkter.
* Kan köras på en enhetsplattform som stöder HLS v3 eller senare, inklusive:

   * PTS-avbrott som markeras med `EXT-X-DISCONTINUITY` taggar
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Körs på en plattform som stöder HTTP-omdirigeringar och JSON-parsning.
* Körs på en plattform som stöder CORS.