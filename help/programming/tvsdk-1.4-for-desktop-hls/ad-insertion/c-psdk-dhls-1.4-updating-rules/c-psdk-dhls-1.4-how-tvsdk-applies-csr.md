---
description: 'null'
seo-description: 'null'
seo-title: Använda kreativa markeringsregler
title: Använda kreativa markeringsregler
uuid: 464c32db-1c96-4d91-97ce-f1d95e57c062
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Använda kreativa markeringsregler{#applying-creative-selection-rules}

TVSDK använder regler för kreativt urval på följande sätt:

* TVSDK tillämpar alla `default`-regler först, följt av de zonspecifika reglerna.
* TVSDK ignorerar alla regler som inte har definierats för det aktuella zon-ID:t.
* När TVSDK tillämpar standardreglerna kan de zonspecifika reglerna ytterligare ändra de kreativa prioriteringarna baserat på `host`-matchningarna (domän) för den kreativitet som valts av `default`-reglerna.

* När TVSDK tillämpar `default`-reglerna i den inkluderade exempelregelfilen med ytterligare zonregler, och om den kreativa domänen M3U8 inte innehåller [!DNL my.domain.com] eller [!DNL a.bcd.com] och annonszonen är `1234`, sorteras de kreativa om och Flash VPAID-kreativiteten spelas upp först om den är tillgänglig. Annars spelas en MP4-annons upp och så vidare ned till JavaScript.

* Om en annonsskapare har valts som TVSDK inte kan spela upp internt ( [!DNL .mp4], [!DNL .flv] osv.) skickar TVSDK en begäran om ompaketering.

Observera att annonstyperna som kan hanteras av TVSDK fortfarande definieras med inställningen `validMimeTypes` i `AuditudeSettings`.
