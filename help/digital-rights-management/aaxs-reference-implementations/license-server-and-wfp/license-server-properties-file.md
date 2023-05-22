---
title: Licensserverns egenskapsfil
description: Licensserverns egenskapsfil
copied-description: true
exl-id: ac105ea6-b5a4-4416-bf17-f619abcf7cd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Licensserverns egenskapsfil {#license-server-properties-file}

Använd [!DNL flashaccess-refimpl.properties] -fil för att konfigurera licensserverkomponenten för referensimplementeringen. Du måste åtminstone konfigurera egenskaperna för transportautentiseringsuppgifterna och licensserverns autentiseringsuppgifter. Platserna för autentiseringsfilerna måste anges i förhållande till katalogen som anges av `config.resourcesDirectory` -egenskap. Den här filen innehåller även flera egenskaper för paketeringsinnehåll: Dessa egenskaper används endast för metadatakonvertering av Flash Media Rights Management Server 1.x. Om du ändrar något av värdena i den här egenskapsfilen måste du starta om licensservern för att ändringarna ska börja gälla.

Nyckelservercertifikatet måste anges i för att det ska gå att skapa licenser för fjärrnyckelleverans till iOS-klienter i Adobe Access [!DNL flashaccess-refimpl.properties].

Följande egenskaper har lagts till i Adobe Access:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Egenskap </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> Key Servers licensservercertifikat, utfärdat av Adobe. Det här certifikatet används för att generera licenser för iOS-enheter när metadata anger att en nyckelserver krävs. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias för Key Servers Adobe-utfärdade licensservercertifikat som lagras på HSM. Använd den här egenskapen i stället för att <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
