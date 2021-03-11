---
description: Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flash. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.
title: StageVideo- och HTML-övertäckningar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# StageVideo- och HTML-övertäckningar{#stagevideo-and-html-overlays}

Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flash. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla visningslisteelement i Flash.

HTML-övertäckningar är gränssnittselement som du kan visa i Flash i visningsplanet på video som återges av `StageVideo` på dess eget plan. Före Flash 15 kunde du inte använda HTML-övertäckningar när maskinvaruacceleration inte var tillgängligt. Från och med Flash 15 visas HTML-övertäckningar när `StageVideo` återgår till programvaruåtergivning.

>[!IMPORTANT]
>
>Beroende på datorns funktioner kan prestanda försämras mer eller mindre när du använder HTML-övertäckningar.

Tänk på följande information:

* I Flash Player 15:

   * Du kan använda HTML-övertäckningar oavsett om maskinvaruacceleration är tillgängligt eller inte.
   * Om du vill använda HTML-övertäckningar anger du `wmode` till `opaque`.

* I Flash Player 14:

   * När maskinvaruacceleration är tillgängligt finns `StageVideo` under visningslistan för Flash, så att du kan använda HTML-övertäckningar.
   * När maskinvaruacceleration inte är tillgängligt återges videon ovanpå alla andra element i webbläsaren, vilket förhindrar att HTML-övertäckningar används.

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

