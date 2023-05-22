---
description: Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning (trickläge) och inkludering av annonsering.
title: Standardbeteende och anpassat uppspelningsbeteende med annonser
exl-id: 56544683-28a3-4720-bfd8-946cb09880aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Standardbeteende och anpassat uppspelningsbeteende med annonser{#default-and-customized-playback-behavior-with-ads}

Medieuppspelningens beteende påverkas av sökning, pausning, snabb framåtspolning eller tillbakaspolning (trickläge) och inkludering av annonsering.

Om du vill åsidosätta standardbeteendet använder du `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>Webbläsarens TVSDK erbjuder inte ett sätt att inaktivera sökning under annonser. Adobe rekommenderar att du konfigurerar programmet så att sökning inaktiveras under annonser.

I följande tabell beskrivs hur Browser TVSDK hanterar annonser och annonsbrytningar under uppspelning:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Videoaktivitet </th> 
   <th colname="col2" class="entry"> Standardbeteendeprincip för webbläsare-TVSDK </th> 
   <th colname="col3" class="entry">Anpassning tillgänglig via <span class="codeph"> AdBreakPolicySelector </span> </th> 
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
   <td colname="col3">Ange en annan princip för annonsbrytningen med <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
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
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen och för den specifika annons som sökningen avslutades med <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över bevakade annonsbrytningar till huvudinnehållet. </td> 
   <td colname="col2"> Om den senaste annonsbrytningen redan har bevakats, hoppar över till den användarvalda sökpositionen. </td> 
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span> och avgöra vilka pauser som redan har bevakats med <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över en eller flera annonsbrytningar och övergår i en bevakad annonsbrytning. </td> 
   <td colname="col2"> Hoppar över annonsbrytningen och söker till positionen omedelbart efter annonsbrytningen. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen (med den bevakade statusen inställd på true) och för den specifika annonsen där sökningen avslutades med hjälp av <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker framåt över annonser som infogats med anpassade annonsmärken. </td> 
   <td colname="col2"> Hoppar till den användarvalda sökpositionen. </td> 
   <td colname="col3">Mer information finns i <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Hantera sökning när sökfältet används</a> </td> 
  </tr> 
 </tbody> 
</table>

## Ställa in anpassade annonseringsbeteenden {#section_custom_ad_behaviors}

Du kan ange vilket beteende du föredrar i annonsinnehållsfabriken i `retrieveAdPolicySelectorCallbackFunc` -metod. Du kan använda `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd`och `selectAdBreaksToPlay` metoder i innehållsfabriken för att välja en princip.
