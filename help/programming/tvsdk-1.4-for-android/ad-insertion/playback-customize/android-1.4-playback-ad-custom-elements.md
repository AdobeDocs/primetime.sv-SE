---
description: TVSDK innehåller klasser och metoder som du kan använda för att anpassa uppspelningsbeteendet för innehåll som innehåller reklam.
title: API-element för annonsuppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# API-element för annonsuppspelning {#api-elements-for-ad-playback}

TVSDK innehåller klasser och metoder som du kan använda för att anpassa uppspelningsbeteendet för innehåll som innehåller reklam.

Följande API-element är användbara för att anpassa uppspelning:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API-element </th> 
   <th colname="col2" class="entry"> Innehåll som stöder reklam </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Ange om en annonsbrytning ska markeras som bevakad av en tittare och, om ja, när den ska markeras. Ange och hämta den bevakade profilen med <span class="codeph"> setAdBreakAsWatched</span> och <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Räknar upp möjliga uppspelningsprinciper för annonsbrytningar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Räknar upp möjliga uppspelningsprinciper för annonser. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Gränssnitt som gör det möjligt att anpassa annonsbeteendet i TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> En klass som implementerar TVSDK-standardbeteendet. Programmet kan åsidosätta den här klassen för att anpassa standardbeteendena utan att implementera hela gränssnittet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span>. <p>Detta är den lokala tidpunkten för uppspelningen, exklusive de monterade annonsbrytningarna. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>Här sker sökningen i förhållande till en lokal tid i strömmen. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>Den virtuella positionen på tidslinjen konverteras till den lokala positionen. </p> </li> 
    </ul> <p>Viktigt:  <span class="codeph"> getLocalTime</span> i <span class="codeph"> MediaPlayer</span> returnerar den aktuella tiden i förhållande till det ursprungliga innehållet, utan dynamiskt uppdelade annonser. <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreakreturns the start time of the break relative to the original content. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty. Anger om tittaren har tittat på annonsen. </td> 
  </tr> 
 </tbody> 
</table>

