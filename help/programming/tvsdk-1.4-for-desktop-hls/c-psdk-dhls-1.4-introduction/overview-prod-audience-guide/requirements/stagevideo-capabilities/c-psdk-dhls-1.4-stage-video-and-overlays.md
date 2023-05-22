---
description: Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flash. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.
title: StageVideo- och HTML-övertäckningar
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo- och HTML-övertäckningar{#stagevideo-and-html-overlays}

Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flash. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.

HTML-övertäckningar är gränssnittselement som du kan visa i visningsplanet i Flash på video som återges av `StageVideo` på sitt eget plan. Före Flash 15 kunde du inte använda HTML-övertäckningar när maskinvaruacceleration inte var tillgängligt. Från och med Flash 15 visas HTML-övertäckningar när `StageVideo` återgår till programvaruåtergivning.

>[!IMPORTANT]
>
>Beroende på datorns kapacitet kan prestanda försämras till en högre eller lägre grad när du använder övertäckningar med HTML.

Tänk på följande information:

* I Flash Player 15:

   * Du kan använda HTML-övertäckningar oavsett om maskinvaruacceleration är tillgängligt eller inte.
   * Om du vill använda HTML-övertäckningar anger du `wmode` till `opaque`.

* I Flash Player 14:

   * När maskinvaruacceleration är tillgänglig `StageVideo` finns under visningslistan för Flash, så du kan använda HTML-övertäckningar.
   * När maskinvaruacceleration inte är tillgängligt återges videon ovanpå alla andra element i webbläsaren, vilket förhindrar användning av övertäckningar med HTML.

Här är de lägsta webbläsarkraven som krävs för att använda HTML-övertäckningar med `StageVideo`:

* Firefox version 4 och senare
* Safari version 4 och senare
* Internet Explorer:

   * Version 9+ i Windows 7 och senare
   * Version 10+ på Windows XP

* Chrome version 26 och senare

   >[!IMPORTANT]
   >
   >Chrome Pepper på Windows XP och Windows Vista stöds inte.
