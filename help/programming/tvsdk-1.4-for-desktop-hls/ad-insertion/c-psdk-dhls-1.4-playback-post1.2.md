---
description: Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning (trickläge) och inkludering av annonsering.
seo-description: Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning (trickläge) och inkludering av annonsering.
seo-title: Standardbeteende och anpassat uppspelningsbeteende med annonser
title: Standardbeteende och anpassat uppspelningsbeteende med annonser
uuid: 45e6b0cd-fb0b-4896-b53a-d3bd78a3c1f3
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Standardbeteende och anpassat uppspelningsbeteende med annonser{#default-and-customized-playback-behavior-with-ads}

Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning (trickläge) och inkludering av annonsering.

Om du vill åsidosätta standardbeteendet använder du `AdPolicySelector`.

>[!IMPORTANT]
>
>TVSDK erbjuder inget sätt att inaktivera sökning under annonser. Adobe rekommenderar att du konfigurerar programmet så att sökning inaktiveras under annonser.

I följande tabell beskrivs hur TVSDK hanterar annonser och annonsbrytningar under uppspelning:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Videoaktivitet </th> 
   <th colname="col2" class="entry"> Standardbeteendeprincip för TVSDK </th> 
   <th colname="col3" class="entry">Anpassning tillgänglig via <span class="codeph"> AdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Under normal uppspelning påträffas en annonsbrytning. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> För live/linjärt spelas annonsbrytningen upp, även om annonsbrytningen redan har bevakats. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">För VOD spelas annonsbrytningen upp och annonsbrytningen markeras som bevakad. </li> 
    </ul> </td> 
   <td colname="col3">Ange en annan princip för annonsbrytningen genom att använda <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker fram över annonsbrytningar till huvudinnehållet. </td> 
   <td colname="col2"> Spelar upp den senaste obevakade annonsbrytningen som hoppats över och återupptar uppspelningen vid önskad sökposition när uppspelningen av brytningar är klar. </td> 
   <td colname="col3">Välj vilken överhoppad brytning som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker bakåt över annonsbrytningar till huvudinnehållet. </td> 
   <td colname="col2"> Hoppar till önskad sökposition utan att lägga till brytningar. </td> 
   <td colname="col3">Välj vilken överhoppad brytning som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker fram till en annonsbrytning. </td> 
   <td colname="col2"> Spelar upp från början av den annons där sökningen avslutades. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen och för den specifika annonsen där sökningen avslutades med <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker bakåt i en annonsbrytning. </td> 
   <td colname="col2"> Spelar upp från början av den annons där sökningen avslutades. </td> 
   <td colname="col3">Ange en annan annonsprincip för annonsbrytningen och för den specifika annons som sökningen avslutades i med <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över bevakade annonsbrytningar till huvudinnehållet. </td> 
   <td colname="col2"> Om den senaste annonsbrytningen redan har bevakats, hoppar över till den användarvalda sökpositionen. </td> 
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span> och ta reda på vilka brytningar som redan har bevakats med <span class="codeph"> TimeLineItem.watch</span>. <p>Viktigt:  Som standard markerar TVSDK en annonsbrytning som bevakad direkt efter att den första annonsen har öppnats i annonsbrytningen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över en eller flera annonsbrytningar och övergår i en bevakad annonsbrytning. </td> 
   <td colname="col2"> Hoppar över annonsbrytningen och söker till positionen omedelbart efter annonsbrytningen. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen (med den bevakade statusen inställd på true) och för den specifika annonsen där sökningen avslutades med <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet går in i trippelläge (DVR-läge). Uppspelningshastigheten kan vara negativ (tillbakaspolning) eller större än 1 (snabbspolning framåt). </td> 
   <td colname="col2"> Hoppar över alla annonser under snabb framåtspolning eller tillbakaspolning, spelar upp den senaste brytningen som hoppats över efter att tricket har spelats upp och hoppar över den av användaren valda trippelpositionen när den pausade uppspelningen är klar. </td> 
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp när tricket slutar med <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker framåt över annonser som infogats med anpassade annonsmärken. </td> 
   <td colname="col2"> Hoppar till den användarvalda sökpositionen. </td> 
   <td colname="col3">Mer information finns i <a href="../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Visa ett söknavigeringsfält med den aktuella uppspelningspositionen..</a> </td> 
  </tr> 
 </tbody> 
</table>

