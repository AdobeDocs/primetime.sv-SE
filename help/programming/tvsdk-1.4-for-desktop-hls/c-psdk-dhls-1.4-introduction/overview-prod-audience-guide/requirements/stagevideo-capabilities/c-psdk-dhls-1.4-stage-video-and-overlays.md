---
description: Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flashen. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla element i visningslistan för Flashar.
title: StageVideo- och HTML-övertäckningar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo- och HTML-övertäckningar{#stagevideo-and-html-overlays}

Du kan använda HTML-övertäckningar med StageVideo för att visa gränssnittselement i videoplanet för visningslistan i Flashen. Det här planet är ovanför StageVideo-planet, så StageVideo visas alltid bakom alla element i visningslistan för Flashar.

HTML-övertäckningar är gränssnittselement som du kan visa i Flashens visningsplan på video som återges av `StageVideo` på sitt eget plan. Före Flash 15 kunde du inte använda HTML-övertäckningar när maskinvaruacceleration inte var tillgängligt. Från och med Flash 15 visas HTML-övertäckningar när `StageVideo` återgår till programvaruåtergivning.

>[!IMPORTANT]
>
>Beroende på datorns kapacitet kan prestanda försämras till en högre eller lägre grad när du använder övertäckningar med HTML.

Tänk på följande information:

* I Flash Player 15:

   * Du kan använda HTML-övertäckningar oavsett om maskinvaruacceleration är tillgängligt eller inte.
   * Om du vill använda HTML-övertäckningar anger du `wmode` till `opaque`.

* I Flash Player 14:

   * När maskinvaruacceleration är tillgänglig `StageVideo` finns under Flashens visningslista, så du kan använda HTML-övertäckningar.
   * När maskinvaruacceleration inte är tillgängligt återges videon ovanpå alla andra element i webbläsaren, vilket förhindrar användning av övertäckningar med HTML.

Här är de lägsta webbläsarkraven för HTML-övertäckningar med `StageVideo`:

* Firefox version 4 och senare
* Safari version 4 och senare
* Internet Explorer:

   * Version 9+ i Windows 7 och senare
   * Version 10+ på Windows XP

* Chrome version 26 och senare

  >[!IMPORTANT]
  >
  >Chrome Pepper på Windows XP och Windows Vista stöds inte.
