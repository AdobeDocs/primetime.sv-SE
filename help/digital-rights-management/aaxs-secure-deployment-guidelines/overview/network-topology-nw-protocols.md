---
title: Nätverksprotokoll som används av Adobe Access
description: Nätverksprotokoll som används av Adobe Access
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Nätverksprotokoll som används av Adobe Access {#network-protocols-used-by-adobe-access}

När du konfigurerar en säker nätverksarkitektur krävs nätverksprotokollen i följande tabell för interaktion mellan Adobe Access och andra system i företagsnätverket.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protokoll </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Använd </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Klienter från Flash Player, Adobe AIR® och Adobe Primetime kommunicerar med Adobe Access via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (valfritt) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player-, Adobe AIR- och Adobe Primetime-klienter kan använda HTTPS för kommunikation med Adobe Access, men HTTPS (SSL) krävs inte såvida du inte behöver stöd för FMRMS 1.x-klienter. Se anmärkningarna i tabellen <a href="network-topology-firewall-rules.md" format="dita" scope="local"> Inkommande URL:er</a> och <a href="network-topology-nw-protocols.md"> Konfigurera SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>