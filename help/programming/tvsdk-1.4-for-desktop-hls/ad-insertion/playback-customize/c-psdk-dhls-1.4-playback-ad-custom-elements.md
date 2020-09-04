---
description: TVSDK innehåller klasser och metoder som du kan använda för att anpassa uppspelningsbeteendet för innehåll som innehåller reklam.
seo-description: TVSDK innehåller klasser och metoder som du kan använda för att anpassa uppspelningsbeteendet för innehåll som innehåller reklam.
seo-title: API-element för annonsuppspelning
title: API-element för annonsuppspelning
uuid: 61ebbfd7-696c-4a5b-8dbb-682770cd5840
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# API-element för annonsuppspelning{#api-elements-for-ad-playback}

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
   <td colname="col2">Ange om en annonsbrytning ska markeras som bevakad av en tittare och, om ja, när den ska markeras. Ange och hämta bevakade profiler med 
    <pre>
     egenskapen <span class="codeph"> adBreakAsWatched</span> .
    </pre> </td> 
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
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Detta är den lokala tidpunkten för uppspelningen, exklusive de monterade annonsbrytningarna. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocal</span>. <p>Här sker sökningen i förhållande till en lokal tid i strömmen. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>Den virtuella positionen på tidslinjen konverteras till den lokala positionen. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Tidslinjeobjekt</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> bevakad</span>. <p>Anger om tittaren har tittat på annonsen. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>Startpositionen och längden på en annonsbrytning eller annons i förhållande till det ursprungliga innehållet. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>Startpositionen och längden på en annonsbrytning eller annons på den virtuella tidslinjen efter att alla placerade annonsbrytningar har beaktats. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

