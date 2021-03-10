---
description: När du konfigurerar en säker nätverksarkitektur krävs nätverksprotokoll för interaktion mellan Adobe Primetime DRM och andra system i företagsnätverket.
title: Adobe Primetime DRM-nätverksprotokoll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Adobe Primetime DRM-nätverksprotokoll {#adobe-primetime-drm-network-protocols}

När du konfigurerar en säker nätverksarkitektur krävs nätverksprotokoll för interaktion mellan Adobe Primetime DRM och andra system i företagsnätverket.

När du konfigurerar en säker nätverksarkitektur krävs följande nätverksprotokoll för den här interaktionen:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protokoll </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Använd </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player-, Adobe AIR®- och Adobe Primetime-klienter kommunicerar med Primetime DRM via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (valfritt) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player-, Adobe AIR- och Adobe Primetime-klienter kan använda HTTPS för att kommunicera med Primetime DRM. HTTPS (SSL) krävs inte såvida du inte har stöd för FMRMS 1.x-klienter. Mer information finns i <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> Inkommande URL:er </a> och Konfigurera SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Portar för programservrar {#ports-for-application-servers}

Du kan konfigurera Adobe Primetime DRM-licensservern så att den använder vilken nätverksport som helst.

Portarna måste aktiveras eller inaktiveras på den inre brandväggen, beroende på vilken nätverksfunktion du vill tillåta för klienter som ansluter till den programserver som kör Primetime DRM.

## Konfigurerar SSL {#configuring-ssl}

SSL (Secure Sockets Layer) är bara nödvändigt om du behöver stöd för Flash Media Rights Management Server 1.x-klienter.

SSL med klientautentisering krävs för nyckelservern för Adobe Primetime DRM. Mer information finns i [Använda Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).