---
title: Använda kreativa markeringsregler
description: Använda kreativa markeringsregler
copied-description: true
exl-id: 756de2e8-ffd0-46f6-9ebc-27e52c5c7b74
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Använda kreativa markeringsregler{#applying-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK använder alla `default` först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteringarna baserat på `host` (domän) matchar på den kreativa som valts av `default` regler.

* När TVSDK använder följande exempelregelfil med ytterligare zonregler `default` regler, om den kreativa domänen M3U8 inte innehåller [!DNL my.domain.com] eller [!DNL a.bcd.com] och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om det går. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonskreatör har valts kan inte TVSDK spela upp internt ( [!DNL .mp4], [!DNL .flv], osv.) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras via `validMimeTypes` ange `AuditudeSettings`.
