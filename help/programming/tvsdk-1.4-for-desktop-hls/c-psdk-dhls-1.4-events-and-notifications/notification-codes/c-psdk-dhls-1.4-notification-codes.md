---
description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-title: Meddelandekoder
title: Meddelandekoder
uuid: a7b77a5c-9873-45cf-8499-aa00270a7ad6
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Översikt {#notification-codes-overview}

TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.

Meddelandeobjekt innehåller information om spelarens status. TVSDK tillhandahåller en kronologiskt sorterad lista med meddelandeobjekt och varje meddelande innehåller följande metadata:

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Element </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> Meddelandetypen. Beroende på plattformen refererar den här egenskapen till en uppräkningstyp med möjliga värden INFO, WARN eller ERROR. Det här är den översta grupperingen för meddelanden. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> kod </td> 
   <td colname="2">Den numeriska representation som tilldelats meddelandet: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Felmeddelandehändelser, från 100000 till 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Varningsmeddelandehändelser, från 200000 till 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Informationshändelser, från 300000 till 399999 </li> 
    </ul> <p>Varje intervall på den översta nivån, t.ex. fel, delas upp i underintervall, t.ex. 101000 till 101999, som representerar uppspelningsfel. </p>
    <pre>
     Uppräkningen <span class="codeph"> mediacore.PSDKErrorCode</span> visar möjliga värden.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">En sträng som innehåller en läsbar beskrivning av koden, till exempel <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadata </td> 
   <td colname="2">Nyckel-/värdepar som innehåller ytterligare relevant information om meddelandet. En nyckel med namnet <span class="codeph"> URL</span> paras till exempel med ett värde som är en URL som är relaterad till meddelandet, till exempel en ogiltig URL som orsakade ett fel. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">En referens till ett annat <span class="codeph"> MediaPlayerNotification</span> -objekt som direkt påverkade det här meddelandet. Ett exempel kan vara ett meddelande om ett fel vid annonsinfogning som direkt motsvarar en konflikt vid en infogning av tidsrader. Alla meddelanden har inte ett internt meddelande. </td> 
  </tr> 
 </tbody> 
</table>

