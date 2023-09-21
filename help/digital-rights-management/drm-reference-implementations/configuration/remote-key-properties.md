---
title: Leveransegenskaper för fjärrnyckel (iOS)
description: Leveransegenskaper för fjärrnyckel (iOS)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Leveransegenskaper för fjärrnyckel (iOS){#remote-key-delivery-properties-ios}

Om du vill ha stöd för generering av licenser för fjärrnyckelleverans till en iOS-klient i Adobe Primetime DRM måste du ange nyckelservercertifikatet i dialogrutan `flashaccess-refimpl.properties` -fil.

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
   <td colname="2" class="- topic/entry "> <p>Aliaset för ett certifikat för en Adobe-utfärdad licensserver som lagras på HSM. </p> <p>När du aktiverar HSM kan du använda den här egenskapen i stället för <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> -egenskap. </p> </td> 
  </tr> 
 </tbody> 
</table>
