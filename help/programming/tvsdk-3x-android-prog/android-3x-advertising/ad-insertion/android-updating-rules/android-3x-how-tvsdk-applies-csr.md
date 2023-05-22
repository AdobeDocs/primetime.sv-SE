---
keywords: regler för kreativt urval;AdobeTVSDKConfig
title: Använd regler för kreativt urval
description: Använd regler för kreativt urval
copied-description: true
exl-id: ec77d3b1-573c-4751-a472-bb9c0aa0b602
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Använd regler för kreativt urval {#apply-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK använder alla `default` först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteringarna baserat på `host` (domän) matchar på den kreativa som valts av `default` regler.

* När TVSDK använder följande exempelregelfil med ytterligare zonregler `default` regler, om den kreativa domänen M3U8 inte innehåller `my.domain.com` eller `a.bcd.com` och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om det går. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonskreatör har valts kan inte TVSDK spela upp internt ( [!DNL .mp4], [!DNL .flv], osv.) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras via `validMimeTypes` ange `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->
