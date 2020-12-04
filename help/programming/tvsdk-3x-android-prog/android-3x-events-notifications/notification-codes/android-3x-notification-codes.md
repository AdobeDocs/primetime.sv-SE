---
description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-title: Meddelandekoder
title: Meddelandekoder
uuid: 6babb203-b6d4-4b11-9fae-41e7db7fd570
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Meddelandekoder {#notification-codes}

TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.

Meddelandeobjekt tillhandahåller information som är relaterad till spelarens status. TVSDK tillhandahåller en kronologiskt sorterad lista med meddelandeobjekt. Varje meddelande innehåller följande metadata:

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Element</b></th> 
   <th colname="2" class="entry"><b> Beskrivning</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>Meddelandetypen. </p> <p>Beroende på plattformen är den här egenskapen en uppräkningstyp med möjliga värden INFO, WARN och ERROR. Det här är den översta grupperingen för meddelanden. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> kod</span> </td> 
   <td colname="2"> <p>Meddelandena tilldelas följande numeriska beteckningar: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Felmeddelandehändelser, från 100000 till 199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Varningsmeddelandehändelser, från 200000 till 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Informationshändelser, från 300000 till 399999 </li> 
     </ul> </p> <p>Varje intervall på den översta nivån, t.ex. fel, delas upp i underintervall, t.ex. 101000 till 101999, som representerar uppspelningsfel. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">En sträng som innehåller en läsbar beskrivning av meddelandehändelsen, till exempel <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadata</span> </td> 
   <td colname="2"> <p>Nyckel-/värdepar som innehåller ytterligare relevant information om meddelandet. </p> <p>En nyckel med namnet <span class="codeph"> URL</span> ger till exempel ett värde som är en URL som är relaterad till meddelandet, till exempel en ogiltig URL som orsakade ett fel. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>En referens till ett annat <span class="codeph"> MediaPlayerNotification</span>-objekt som direkt påverkade det här meddelandet. </p> <p>Ett exempel kan vara ett meddelande om ett fel vid annonsinfogning som direkt motsvarar en konflikt vid en infogning av tidsrader. Alla meddelanden har inte ett internt meddelande. </p> </td> 
  </tr> 
 </tbody> 
</table>