---
description: Dessa klasser innehåller information om tidslinjen för ett visst medium, inklusive placering av annonser.
seo-description: Dessa klasser innehåller information om tidslinjen för ett visst medium, inklusive placering av annonser.
seo-title: Klasser för tidslinje
title: Klasser för tidslinje
uuid: 9c06fec1-d725-4fe8-9cf5-1e3ade2b7d27
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Tidslinjeklasser{#timeline-classes}

Dessa klasser innehåller information om tidslinjen för ett visst medium, inklusive placering av annonser.

Paket: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Namn </th> 
   <th colname="2" class="entry"> <p>Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker  </a> </span> </td> 
   <td colname="2"> Gränssnitt som definierar det protokoll som du måste implementera om du vill skapa en innehållsspårningsmodul som är utformad för att integreras med TVSDK-biblioteket. <p>Det här gränssnittet kräver att du definierar hur förloppshändelser rapporteras till fjärrspårningssystemet. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> Möjligheter  </a> </span> </td> 
   <td colname="2"> Basklass för alla affärsmöjlighetsklasser. En affärsmöjlighetsklass representerar en"intressant" punkt på tidslinjen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Placement  </a> </span> </td> 
   <td colname="2"> En klass som omsluter information om placering av tidslinjen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode  </a> </span> </td> 
   <td colname="2"> Uppräkning av placeringslägen, t.ex. om innehåll ska infogas eller ersättas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType  </a> </span> </td> 
   <td colname="2"> Uppräkning av placeringstyper som anger var placering görs på tidslinjen. till exempel PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Reservation  </a> </span> </td> 
   <td colname="2"> En reservation används för att begränsa eller förhindra vidare bearbetning av ett visst tidsintervall på tidslinjen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Tidslinje  </a> </span> </td> 
   <td colname="2"> Gränssnitt som innehåller en iterator för bearbetning av tidslinjemarkörer. Representerar innehållets tidslinje, inklusive annonsbrytningar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> Tidslinjeobjekt  </a> </span> </td> 
   <td colname="2"> Klass. Allmän oföränderlig representation av ett tidslinjeobjekt. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TidslinjeMarkör  </a> </span> </td> 
   <td colname="2"> En klass som representerar en markör på tidslinjen. Detta är ett intresseområde på den faktiska tidslinjen. För närvarande är de områden som är intressanta annonser, som du kanske vill markera med en annan färg i navigeringsfältets gränssnitt. Varje markör definieras av en position och en varaktighet (alla uttrycks i millisekunder). </td> 
  </tr> 
 </tbody> 
</table>

