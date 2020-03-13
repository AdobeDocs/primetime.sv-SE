---
description: TVSDK har för närvarande inbyggt stöd för annonsleverantörens metadata för TVSDK-annonser, direkta annonsbrytningar och anpassade annonsmarkörer.
seo-description: TVSDK har för närvarande inbyggt stöd för annonsleverantörens metadata för TVSDK-annonser, direkta annonsbrytningar och anpassade annonsmarkörer.
seo-title: Annonsinfogningstyper
title: Annonsinfogningstyper
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Annonsinfogningstyper {#ad-insertion-types}

TVSDK har för närvarande inbyggt stöd för annonsleverantörens metadata för TVSDK-annonser, direkta annonsbrytningar och anpassade annonsmarkörer.

Det stöder följande typer av arbetsflöden för annonsinfogning för VOD och direktsänt/linjärt innehåll.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Infogningstyp </th> 
   <th colname="col2" class="entry"> Stöds i... </th> 
   <th colname="col3" class="entry"> Beskrivning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Annonser om annonsbeslut i Adobe Primetime </td> 
   <td colname="col2">VOD <p>Live </p> <p>Linjär </p> </td> 
   <td colname="col3">Referensimplementeringen tillhandahåller <span class="codeph"> AuditudeMetadata</span> -information som ansluter till servern för Primetime-annonsbeslut (tidigare Auditude), baserat på informationen som anges i delen</a> Primetime-annonser i JSON-konfigurationsfilen</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Direktreklam </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Du måste ange annons-URL:er i JSON-indatafilen. När TVSDK försöker lösa en annons anropas den direkta annonsbrytningslösaren och annonserna löses baserat på informationen om direkta annonsbrytningar i JSON-konfigurationsfilen</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Anpassade annonsmarkörer </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Anpassade annonsmarkörer är användbara när videoflödet innehåller både huvudinnehåll och annonser, men inte innehåller information om annonsplacering och -timing. Om annonspositioneringsinformationen hämtas på ett annat sätt, till exempel via ett externt CMS-system, kan du definiera anpassade annonsmarkörer och skicka dem till spelarens tidslinje. <p>Om du vill konfigurera en spelare för annonsinfogning måste du skicka annonsmetadata i det anpassade avsnittet med annonseringsmetadata i JSON-konfigurationsfilen</a>, som har en implementering som stöds i referensimplementeringen. </p> </td>
  </tr>
 </tbody>
</table>