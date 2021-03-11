---
description: Innehållet i en AdAsset beskriver en tilläggsbanderoll.
title: Kompletterande banderolldata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Kompletterande banderolldata {#companion-banner-data}

Innehållet i en AdAsset beskriver en tilläggsbanderoll.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Var `AdAsset` innehåller information om hur resursen visas.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tillgänglig information </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Bredden på den tillhörande banderollen i pixlar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Den kompletterande banderollens höjd i pixlar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> resurstyp </td> 
   <td colname="col2">Resurstypen för den här tilläggsbanderollen: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Data finns i HTML-kod. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Data är en iframe-URL (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> statisk URL </td> 
   <td colname="col2"> <p>Ibland har den tillhörande banderollen också en <span class="codeph"> staticURL</span> som är en direkt URL till bilden eller till en <span class="codeph"> .swf</span> (flash banner). </p> <p>Om du inte vill använda html eller iframe kan du använda en direkt URL till en bild eller swf för att visa banderollen på scenen Flash i stället. I det här fallet kan du använda den statiska URL:en <span class="codeph"></span> för att visa banderollen. </p> <p>Viktigt:  Du måste kontrollera om den statiska URL:en är en giltig sträng, eftersom den här egenskapen kanske inte alltid är tillgänglig. </p> </td> 
  </tr> 
 </tbody> 
</table>

