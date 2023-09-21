---
description: Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning samt reklam.
title: Standardbeteende och anpassat uppspelningsbeteende med annonser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Standardbeteende och anpassat uppspelningsbeteende med annonser {#default-and-customized-playback-behavior-with-ads}

Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning samt reklam.

Om du vill åsidosätta standardbeteendet använder du `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>TVSDK erbjuder inget sätt att inaktivera sökning under annonser. Adobe rekommenderar att du konfigurerar programmet så att sökning inaktiveras under annonser.

Här är uppspelningsbeteendet för direktsänt/linjärt innehåll:

* Om du återupptar uppspelningen efter en paus spelas innehållet upp som buffrades vid tiden för paus.

  Om den återupptagna positionen fortfarande finns i uppspelningsintervallet ska uppspelningen vara kontinuerlig. Annars hoppar TVSDK till den nya direktpunkten. Du kan också utföra en sökåtgärd och välja en annan uppspelningspunkt.
* TVSDK löser annonser mellan indikeringar efter den position där programmet kommer in i direktuppspelningen.

  Uppspelningen börjar efter att den första referensen har lösts. Standardvärdet för att ange direktuppspelning är klientens direktpunkt, men du kan välja en annan position. Alla ledtrådar före den inledande positionen löses efter att programmet har utfört en sökning i DVR-fönstret.

I följande tabell beskrivs hur TVSDK hanterar annonser och annonsbrytningar under uppspelning:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Videoaktivitet</b> </th> 
   <th colname="col2" class="entry"> <b>Standardbeteendeprincip för TVSDK</b> </th> 
   <th colname="col3" class="entry"><b>Anpassning tillgänglig via <span class="codeph"> AdBreakPolicySelector</b></span> </th> 
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
   <td colname="col3">Välj vilken överhoppad brytning som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker fram till en annonsbrytning. </td> 
   <td colname="col2"> Spelar upp från början av den annons där sökningen avslutades. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen och för den specifika annonsen där sökningen avslutades med hjälp av <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker bakåt i en annonsbrytning. </td> 
   <td colname="col2"> Spelar upp från början av den annons där sökningen avslutades. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen och för den specifika annonsen där sökningen avslutades med hjälp av <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över bevakade annonsbrytningar till huvudinnehållet. </td> 
   <td colname="col2"> Om den senaste annonsbrytningen redan har bevakats, hoppar över till den användarvalda sökpositionen. </td> 
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span> och avgöra vilka pauser som redan har bevakats med <span class="codeph"> AdBreak.isWatched</span> . <p>Viktigt: Som standard markerar TVSDK en annonsbrytning som bevakad omedelbart efter att den första annonsen har öppnats. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över en eller flera annonsbrytningar och övergår i en bevakad annonsbrytning. </td> 
   <td colname="col2"> Hoppar över annonsbrytningen och söker till positionen omedelbart efter annonsbrytningen. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen (med den bevakade statusen inställd på true) och för den specifika annonsen där sökningen avslutades med hjälp av <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet går in i trippelläge (DVR-läge). Uppspelningshastigheten kan vara negativ (tillbakaspolning) eller större än 1 (snabb framåt). </td> 
   <td colname="col2"> Hoppar över alla annonser under snabb framåtspolning eller tillbakaspolning, spelar upp den senaste brytningen som hoppats över efter att tricket har spelats upp och hoppar över den av användaren valda trippelpositionen när den pausade uppspelningen är klar. </td> 
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp när tricket slutar med <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker framåt över annonser som infogats med anpassade annonsmärken. </td> 
   <td colname="col2"> Hoppar till den användarvalda sökpositionen. </td> 
   <td colname="col3">Mer information finns i <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Visa ett söknavigeringsfält med aktuell uppspelningsposition</a>. </td> 
  </tr> 
 </tbody> 
</table>
