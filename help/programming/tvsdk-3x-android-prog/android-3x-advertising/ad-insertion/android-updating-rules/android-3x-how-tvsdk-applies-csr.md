---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Använd regler för kreativt urval
title: Använd regler för kreativt urval
uuid: 66e55f95-25ce-4838-b222-63ee34e535d1
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Använd regler för kreativt urval {#apply-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK tillämpar alla `default`-regler först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteringarna baserat på `host`-matchningarna (domän) för den kreativitet som valts av `default`-reglerna.

* När TVSDK tillämpar `default`-reglerna i den inkluderade exempelregelfilen med ytterligare zonregler, och om den kreativa domänen M3U8 inte innehåller `my.domain.com` eller `a.bcd.com` och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om den är tillgänglig. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonsskapare har valts som TVSDK inte kan spela upp internt ( [!DNL .mp4], [!DNL .flv] osv.) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras med inställningen `validMimeTypes` i `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

