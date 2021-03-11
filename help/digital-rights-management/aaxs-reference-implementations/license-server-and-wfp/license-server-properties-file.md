---
title: Licensserverns egenskapsfil
description: Licensserverns egenskapsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Licensserverns egenskapsfil {#license-server-properties-file}

Använd filen [!DNL flashaccess-refimpl.properties] för att konfigurera licensserverkomponenten för referensimplementeringen. Du måste åtminstone konfigurera egenskaperna för transportautentiseringsuppgifterna och licensserverns autentiseringsuppgifter. Platserna för autentiseringsfilerna måste anges i förhållande till katalogen som anges av egenskapen `config.resourcesDirectory`. Den här filen innehåller även flera egenskaper för paketeringsinnehåll: Dessa egenskaper används endast för metadatakonvertering av Flash Media Rights Management Server 1.x. Om du ändrar något av värdena i den här egenskapsfilen måste du starta om licensservern för att ändringarna ska börja gälla.

Om du vill ha stöd för generering av licenser för fjärrnyckelleverans till iOS-klienter i Adobe Access måste nyckelservercertifikatet anges i [!DNL flashaccess-refimpl.properties].

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

