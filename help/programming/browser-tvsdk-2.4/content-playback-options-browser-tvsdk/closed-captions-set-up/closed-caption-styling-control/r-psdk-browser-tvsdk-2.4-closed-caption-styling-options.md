---
description: Du kan ange flera alternativ för bildtextformat och de här alternativen åsidosätter formatalternativen i de ursprungliga bildtexterna.
seo-description: Du kan ange flera alternativ för bildtextformat och de här alternativen åsidosätter formatalternativen i de ursprungliga bildtexterna.
seo-title: Alternativ för textningsformat
title: Alternativ för textningsformat
uuid: 0e2fd9f3-e569-4b5d-9b78-86f8ee6230ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Alternativ för textningsformat{#closed-caption-styling-options}

Du kan ange flera alternativ för bildtextformat och de här alternativen åsidosätter formatalternativen i de ursprungliga bildtexterna.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>I alternativ som definierar standardvärden (till exempel `DEFAULT`) refererar det värdet till inställningen som var när bildtexten ursprungligen angavs.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Format </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Teckensnitt </td> 
   <td colname="2"> <p>Teckensnittstypen. </p> <p>Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Font </span> och representerar till exempel fast teckenbredd med eller utan serifer. </p> <p>Tips:  De faktiska teckensnitten som finns på en enhet kan variera, och ersättningar används vid behov. Monospace med serifer används vanligtvis som ersättning, men den här ersättningen kan vara systemspecifik. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Storlek </td> 
   <td colname="2"> <p>Bildtextens storlek. </p> <p> Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Size </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM  </span> - Standardstorlek </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> STOR  </span> - Cirka 30 % större än mediet </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL  </span> - Cirka 30 % mindre än medium </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> STANDARD  </span> - Bildtextens standardstorlek; samma som medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Teckenfärg </td> 
   <td colname="2"> <p>Teckenfärgen. </p> <p>Kan endast anges till ett värde som definieras av uppräkningen <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bakgrundsfärg </td> 
   <td colname="2"> <p>Bakgrundsteckencellens färg. </p> <p>Kan endast anges med värden som är tillgängliga för teckensnittsfärgen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Ogenomskinlighet för teckensnitt </td> 
   <td colname="2"> <p>Textens opacitet. </p> <p>Uttryckt som en procentandel från 0 (helt genomskinlig) till 100 (helt ogenomskinlig). <span class="codeph"> DEFAULT_OPACITY  </span> för teckensnittet är 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Nedre indrag </td> 
   <td colname="2"> <p>Lodrätt avstånd från underkanten av bildtextfönstret för bildtexter som ska undvikas. </p> <p>Uttrycks som en procentandel av bildtextfönstrets höjd (till exempel "20%") eller ett antal pixlar (till exempel "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Säkert område </td> 
   <td colname="2"> <p>Ett område runt skärmens kant på mellan 0 % och 25 % där bildtexter inte visas. </p> <p>Som standard är det säkra området för 608/708 12 % och det säkra området för WebVTT 0 %. Med den här inställningen kan programmet åsidosätta den standardinställningen. Om två värden anges, till exempel strängen "10%,20%", är det första värdet det vågräta säkra området och det andra värdet det lodräta säkra området. Om ett värde anges, till exempel strängen "15%", används det angivna säkra området både för den lodräta och vågräta axeln. </p> </td> 
  </tr> 
 </tbody> 
</table>

