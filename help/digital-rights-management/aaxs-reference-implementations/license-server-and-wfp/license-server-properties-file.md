---
seo-title: Licensserverns egenskapsfil
title: Licensserverns egenskapsfil
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Licensserverns egenskapsfil {#license-server-properties-file}

Använd [!DNL flashaccess-refimpl.properties] filen för att konfigurera licensserverkomponenten för referensimplementeringen. Du måste åtminstone konfigurera egenskaperna för transportautentiseringsuppgifterna och licensserverns autentiseringsuppgifter. Platserna för autentiseringsfilerna måste anges i förhållande till katalogen som anges av `config.resourcesDirectory` egenskapen. Den här filen innehåller även flera egenskaper för paketeringsinnehåll: dessa egenskaper används endast för Flash Media Rights Management Server 1.x-metadatakonvertering. Om du ändrar något av värdena i den här egenskapsfilen måste du starta om licensservern för att ändringarna ska börja gälla.

Nyckelservercertifikatet måste anges i [!DNL flashaccess-refimpl.properties]om du vill ha stöd för generering av licenser för fjärrnyckelleverans till iOS-klienter i Adobe Access.

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
   <td colname="2" class="- topic/entry ">Alias för Key Servers Adobe-utfärdade licensservercertifikat som lagras på HSM. När HSM är aktiverat använder du den här egenskapen i stället för <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>

