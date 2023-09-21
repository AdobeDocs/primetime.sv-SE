---
title: Använda kreativa markeringsregler
description: Använda kreativa markeringsregler
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Använda kreativa markeringsregler{#applying-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK använder alla `default` först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteringarna baserat på `host` (domän) matchar på den kreativa som valts av `default` regler.

* När TVSDK använder följande exempelregelfil med ytterligare zonregler `default` regler, om M3U8-domänen inte innehåller [!DNL my.domain.com] eller [!DNL a.bcd.com] och annonszonen är `1234`, sorteras de kreativa om och Flashens VPAID-kreativa spelas upp först om det går. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonskreatör har valts kan inte TVSDK spela upp internt ( [!DNL .mp4], [!DNL .flv], osv.) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras via `validMimeTypes` ställa in `AuditudeSettings`.
