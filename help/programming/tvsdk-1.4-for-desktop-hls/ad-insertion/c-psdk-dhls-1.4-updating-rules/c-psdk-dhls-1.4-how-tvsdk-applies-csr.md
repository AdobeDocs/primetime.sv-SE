---
description: 'null'
seo-description: 'null'
seo-title: Använda kreativa markeringsregler
title: Använda kreativa markeringsregler
uuid: 464c32db-1c96-4d91-97ce-f1d95e57c062
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Använda kreativa markeringsregler{#applying-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK tillämpar alla `default` regler först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteterna baserat på matchningen `host` (domän) för den kreativitet som valts enligt `default` reglerna.

* I den inkluderade exempelregelfilen med ytterligare zonregler, när TVSDK tillämpar `default` reglerna, och om den kreativa domänen M3U8 inte innehåller [!DNL my.domain.com] eller [!DNL a.bcd.com] och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om det är tillgängligt. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonskreatör har valts som TVSDK inte kan spela upp internt ( [!DNL .mp4], [!DNL .flv]etc) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras via inställningen i `validMimeTypes` . `AuditudeSettings`20000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
