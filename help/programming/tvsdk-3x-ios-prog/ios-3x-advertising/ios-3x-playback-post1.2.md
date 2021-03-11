---
description: Medieuppspelningens beteende påverkas av sökning, pausning och infogning av annonsering.
title: Standardbeteende och anpassat uppspelningsbeteende med annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Standardbeteende och anpassat uppspelningsbeteende med annonser {#default-and-customized-playback-behavior-with-ads}

Medieuppspelningens beteende påverkas av sökning, pausning och infogning av annonsering.

Om du vill åsidosätta standardbeteendet använder du `PTAdPolicySelector`.

>[!IMPORTANT]
>
>För VOD och direktuppspelning/linjär direktuppspelning kan tidslinjejusteringar inte revideras. Det innebär att en annons inte kan tas bort från tidslinjen efter att den har spelats upp. Om användaren söker tillbaka spelas samma annons upp igen, även om den normala principen skulle ha varit att ta bort den.

>[!IMPORTANT]
>
>TVSDK erbjuder inget sätt att inaktivera sökning under annonser. Adobe rekommenderar att du konfigurerar programmet så att sökning inaktiveras under annonser.

I följande tabell beskrivs hur TVSDK hanterar annonser och annonsbrytningar under uppspelning:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Videoaktivitet</b></th> 
   <th colname="col2" class="entry"><b>Standardbeteendeprincip för TVSDK</b></th> 
   <th colname="col3" class="entry"><b>Anpassning tillgänglig via PTAdPolicySelector</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Under normal uppspelning påträffas en annonsbrytning. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Välj vilken av de överhoppade brytningarna som ska spelas upp med <span class="codeph"> selectAdBreaksToPlay</span> och ta reda på vilka brytningar som redan har bevakats med <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Viktigt:  Som standard markerar TVSDK en annonsbrytning som bevakad direkt efter att den första annonsen har öppnats i annonsbrytningen. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Programmet söker framåt eller bakåt över en eller flera annonsbrytningar och övergår i en bevakad annonsbrytning. </td> 
   <td colname="col2"> Hoppar över annonsbrytningen och söker till positionen omedelbart efter annonsbrytningen. </td> 
   <td colname="col3">Ange en annan annonspolicy för annonsbrytningen (med den bevakade statusen inställd på true) och för den specifika annonsen där sökningen avslutades med <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ditt program söker framåt över annonser som infogats med anpassade annonsmärken. </td> 
   <td colname="col2"> Hoppar till den användarvalda sökpositionen. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>