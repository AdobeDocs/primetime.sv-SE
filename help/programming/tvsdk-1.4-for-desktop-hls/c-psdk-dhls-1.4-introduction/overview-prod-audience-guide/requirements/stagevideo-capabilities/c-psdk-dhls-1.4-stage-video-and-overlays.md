---
description: Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i Flash-visningslistans videoplan. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.
seo-description: Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i Flash-visningslistans videoplan. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.
seo-title: StageVideo- och HTML-övertäckningar
title: StageVideo- och HTML-övertäckningar
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo- och HTML-övertäckningar{#stagevideo-and-html-overlays}

Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i Flash-visningslistans videoplan. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.

HTML-övertäckningar är gränssnittselement som du kan visa i Flash-visningsplanet på video som återges av `StageVideo` på ett eget plan. Före Flash 15 kunde du inte använda HTML-övertäckningar när maskinvaruacceleration inte var tillgängligt. Från och med Flash 15 visas HTML-övertäckningar när de `StageVideo` återgår till programvaruåtergivning.

>[!IMPORTANT]
>
>Beroende på datorns funktioner kan prestanda försämras mer eller mindre när du använder HTML-övertäckningar.

Tänk på följande information:

* I Flash Player 15:

   * Du kan använda HTML-övertäckningar oavsett om maskinvaruacceleration är tillgängligt eller inte.
   * Om du vill använda HTML-övertäckningar anger du `wmode` till `opaque`.

* I Flash Player 14:

   * När maskinvaruacceleration är tillgängligt finns det `StageVideo` nedanför visningslistan i Flash, så att du kan använda HTML-övertäckningar.
   * När maskinvaruacceleration inte är tillgängligt återges videon ovanpå alla andra element i webbläsaren, vilket förhindrar att HTML-övertäckningar används.

Här är de lägsta webbläsarkraven för att använda HTML-övertäckningar med `StageVideo`:

* Firefox version 4 och senare
* Safari version 4 och senare
* Internet Explorer:

   * Version 9+ i Windows 7 och senare
   * Version 10+ på Windows XP

* Chrome version 26 och senare

   >[!IMPORTANT]
   >
   >Chrome Pepper på Windows XP och Windows Vista stöds inte.

