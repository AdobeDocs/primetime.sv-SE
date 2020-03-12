---
description: Innehållet i en AdBannerAsset beskriver en tilläggsbanderoll.
seo-description: Innehållet i en AdBannerAsset beskriver en tilläggsbanderoll.
seo-title: Kompletterande banderolldata
title: Kompletterande banderolldata
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Kompletterande banderolldata{#companion-banner-data}

Innehållet i en AdBannerAsset beskriver en tilläggsbanderoll.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Händelsen `AdobePSDK.PSDKEventType.AD_STARTED` returnerar en `Ad` instans som innehåller en `companionAssets` egenskap ( `Array<AdBannerAsset>`).
Var och en `AdBannerAsset` innehåller information om hur resursen visas.

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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">statisk: Data är en statisk bild-URL (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <ph>
      banderolldata
    </ph> </td> 
   <td colname="col2"> Data av den typ som anges av <span class="codeph"> resourceType</span> för den här tilläggsbanderollen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> statisk URL </td> 
   <td colname="col2"> <p>Ibland kan den tillhörande banderollen också ha en statisk URL som är en direkt URL till bilden. </p> <p>Om du inte vill använda html eller iframe kan du använda en direkt URL till en bild. I det här fallet kan du använda staticURL för att visa banderollen. </p> <p>Viktigt:  Du måste kontrollera om den statiska URL:en är en giltig sträng, eftersom den här egenskapen kanske inte alltid är tillgänglig. </p> </td> 
  </tr> 
 </tbody> 
</table>

