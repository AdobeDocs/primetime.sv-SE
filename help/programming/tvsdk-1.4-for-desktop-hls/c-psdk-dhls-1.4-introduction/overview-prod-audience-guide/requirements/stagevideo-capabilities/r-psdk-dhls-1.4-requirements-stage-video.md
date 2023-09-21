---
description: På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video direkt på enhetens maskinvara.
title: Lägsta krav för StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Lägsta krav för StageVideo{#stagevideo-minimum-requirements}

På enheter som stöder GPU-acceleration (maskinvara) kan du använda ett flash.media.StageVideo-objekt för att bearbeta video direkt på enhetens maskinvara.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

En kombination av olika faktorer avgör när och hur du kan använda `StageVideo`. I följande tabell visas en ögonblicksbild av några av de krav och begränsningar som är kopplade till användningen av StageVideo. Dessa krav och begränsningar kan komma att ändras.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plattform </th> 
   <th colname="col2" class="entry"> Windows och Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Minst Flash 10.1 eller senare </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Flash 15 och senare för reservfunktionen till programvara </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Webbläsare och <span class="codeph"> wmode</span> inställningar </td> 
   <td colname="col2"> <p><b>På Flash 15</b>, ange <span class="codeph"> wmode=opaque</span> så att du kan använda HTML-övertäckningar. </p> <p>Följande webbläsare stöder för närvarande inte maskinvaruacceleration: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox på Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome före 26 och alla versioner av Chrome i Windows XP och Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (alla versioner) </li> 
     </ul>Andra kombinationer av webbläsare/operativsystem kan förhindra åtkomst till maskinvaruacceleration. I dessa scenarier <span class="codeph"> StageVideo</span> använder programvara med negativ inverkan på prestanda. </p> <p><b>På Flash 14 och tidigare</b>om webbläsaren inte stöder maskinvaruacceleration kan spelaren återge Flashen direkt till grafikprocessorn, men ange <span class="codeph"> wmode=direct</span> för att aktivera den här återgivningen. <p>Tips! GPU-drivrutiner som är äldre än 2009 kan behöva uppdateras eftersom dessa drivrutiner kanske saknar stöd för maskinvaruacceleration. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream-objekt </td> 
   <td colname="col2">The <span class="codeph"> StageVideoEvent.RENDER_STATE</span> -händelsen skickas inte om du inte kopplar en <span class="codeph"> NetStream</span> objekt till <span class="codeph"> StageVideo</span> -objekt. </td> 
  </tr> 
 </tbody> 
</table>
