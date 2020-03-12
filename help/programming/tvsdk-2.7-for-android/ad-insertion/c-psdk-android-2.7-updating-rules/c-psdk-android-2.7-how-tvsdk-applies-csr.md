---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: Använd regler för kreativt urval
title: Använd regler för kreativt urval
uuid: 75109483-ea60-43a8-92e7-4bcba48986bc
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Använd regler för kreativt urval {#apply-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK tillämpar alla `default` regler först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteterna baserat på matchningen `host` (domän) för den kreativitet som valts enligt `default` reglerna.

* I den inkluderade exempelregelfilen med ytterligare zonregler, när TVSDK tillämpar `default` reglerna, och om den kreativa domänen M3U8 inte innehåller [!DNL my.domain.com] eller [!DNL a.bcd.com] och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om det är tillgängligt. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonskreatör har valts som TVSDK inte kan spela upp internt ( [!DNL .mp4], [!DNL .flv]etc) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras via inställningen i `validMimeTypes` . `AuditudeSettings`20000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

