---
title: Säkerhet för nätverkslager
description: Säkerhet för nätverkslager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Säkerhet för nätverkslager{#network-layer-security}

Säkerhetsluckor för nätverk är bland de första hoten mot alla Internetanslutna eller intranätriktade programservrar. I det här avsnittet beskrivs processen att härja värdar i nätverket mot dessa sårbarheter. Den behandlar nätverkssegmentering, TCP/IP-stackhärdning (Transmission Control Protocol/Internet Protocol) och användning av brandväggar för värdskydd.

I den här tabellen beskrivs vanliga tekniker som minskar säkerhetsluckor i nätverk.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Teknik </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">DMZ (Demilitarized Zone) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Segmentering måste finnas på minst två nivåer med programservern som används för att köra Adobe Access bakom den inre brandväggen. Skilj det externa nätverket från det DMZ som innehåller webbservrarna, som i sin tur måste separeras från det interna nätverket. Använd brandväggar för att implementera separationslagren. Kategorisera och kontrollera den trafik som passerar genom varje nätverkslager för att säkerställa att endast absolut minimum av nödvändiga data tillåts. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Privata IP-adresser </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd NAT (Network Address Translation) med privata RFC 1918-IP-adresser på programservrar för Adobe Access. Tilldela privata IP-adresser (10.0.0.0/8, 172.16.0.0/12 och 192.168.0.0/16) för att göra det svårare för en angripare att dirigera trafik till och från en intern NAT-värd via Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Brandväggar </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd följande kriterier för att välja en brandväggslösning: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implementera brandväggar med stöd för proxyservrar och/eller tillståndskänsliga kontroller istället för enkla paketfiltreringslösningar. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Använd en brandvägg som har stöd för ett säkerhetsparadigm där du kan neka alla tjänster utom de som uttryckligen tillåts. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implementera en brandväggslösning som är dubbel-homed eller multihomed. Arkitekturen ger den högsta säkerhetsnivån och hjälper till att förhindra att obehöriga kringgår brandväggens säkerhet. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

