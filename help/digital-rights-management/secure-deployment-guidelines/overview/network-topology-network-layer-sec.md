---
description: Säkerhetsluckor för nätverk är bland de första hoten mot alla Internetanslutna eller intranätriktade programservrar, och du måste värdar i nätverket mot dessa sårbarheter.
seo-description: Säkerhetsluckor för nätverk är bland de första hoten mot alla Internetanslutna eller intranätriktade programservrar, och du måste värdar i nätverket mot dessa sårbarheter.
seo-title: Säkerhet för nätverkslager
title: Säkerhet för nätverkslager
uuid: c750c595-a784-47ce-be0b-17b8d60c5753
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Säkerhet för nätverkslager{#network-layer-security}

Säkerhetsluckor för nätverk är bland de första hoten mot alla Internetanslutna eller intranätriktade programservrar, och du måste värdar i nätverket mot dessa sårbarheter.

Här är några vanliga tekniker som minskar sårbarheten när det gäller nätverkssäkerhet:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Teknik </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">DMZ (Demilitarized Zone) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Segmentering måste finnas på minst två nivåer med den programserver som används för att köra Adobe Primetime DRM när Primetime DRM ligger bakom den inre brandväggen. Du måste separera det externa nätverket från det DMZ som innehåller webbservrarna, och webbservrarna måste separeras från det interna nätverket. Du kan använda brandväggar för att implementera dessa separationslager. </p> <p>Du kan kategorisera och styra den trafik som passerar genom varje nätverkslager för att säkerställa att endast absolut minimum av obligatoriska data tillåts. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Privata IP-adresser </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd NAT (Network Address Translation) med privata RFC 1918-IP-adresser på Primetime DRM-programservrar. Du kan tilldela privata IP-adresser (10.0.0.0/8, 172.16.0.0/12 och 192.168.0.0/16) för att göra det svårare för en angripare att dirigera trafik till och från en intern NAT-värd via Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Brandväggar </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Här följer några kriterier att tänka på när du väljer en brandväggslösning: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implementera brandväggar med stöd för proxyservrar och/eller tillståndskänsliga kontroller istället för enkla paketfiltreringslösningar. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Använd en brandvägg som har stöd för ett säkerhetsparadigm där du kan neka alla tjänster, förutom explicit tillåtna tjänster. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implementera en brandväggslösning som är dubbel-homed eller multihomed. Arkitekturen ger den högsta säkerhetsnivån och förhindrar obehöriga användare att kringgå brandväggens säkerhet. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

