---
description: 'null'
seo-description: 'null'
seo-title: Leveransegenskaper för fjärrnyckel (iOS)
title: Leveransegenskaper för fjärrnyckel (iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Leveransegenskaper för fjärrnyckel (iOS){#remote-key-delivery-properties-ios}

Om du vill ha stöd för generering av licenser för fjärrnyckelleverans till en iOS-klient i Adobe Primetime DRM måste du ange nyckelservercertifikatet i `flashaccess-refimpl.properties` filen.

Följande egenskaper har lagts till i Primetime DRM:

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
   <td colname="2" class="- topic/entry "> <p>Key Servers licensservercertifikat som utfärdas av Adobe. </p> <p>Det här certifikatet genererar licenser för iOS-enheter när metadata anger att en nyckelserver krävs. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Aliaset för Key Servers Adobe-utfärdade licensservercertifikat som lagras på HSM. </p> <p>När du aktiverar HSM kan du använda den här egenskapen i stället för egenskapen <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

