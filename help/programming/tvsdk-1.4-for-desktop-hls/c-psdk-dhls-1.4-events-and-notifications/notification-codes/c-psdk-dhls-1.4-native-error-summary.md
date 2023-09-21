---
title: Information om NATIVE_ERROR-meddelandet
description: Information om NATIVE_ERROR-meddelandet
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Information om NATIVE_ERROR-meddelandet {#details-for-the-native-error-notification}

När TVSDK hanterar ett systemspecifikt fel anges några eller alla följande metadatanyckelvärden.

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Namn på metadatanyckel </th> 
   <th colname="col2" class="entry"> Metadatavärde </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      Inbyggd felkod från Flashen Player. 
    </pre> Dessa koder representerar följande: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM-fel (koderna 3300 till 3367). Detta är samma som motsvarande felkoder för Flash Player. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Videouppspelningsfel (-1 till 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Kryptografifel (300 till 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_CODE_MESSAGE </span> </td> 
   <td colname="col2"> En sträng som innehåller felets namn, till exempel <span class="codeph"> AAXS_InvalidVoucher </span> eller <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RUNTIME_SUBERROR_CODE </span> </td> 
   <td colname="col2"> För DRM-fel returneras även underfelkoder. Dessa koder motsvarar <span class="codeph"> DRMErrorEvents </span> suberror-kod som returneras av Flashen Player. När du rapporterar fel till Adobe ska du inkludera det här numeriska värdet för felsökningshjälp. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> För DRM är detta den anpassade felsträngen från DRM-serverdistributionen, om du har definierat någon. Inkludera även detta när du rapporterar fel till Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> BESKRIVNING </span> </td> 
   <td colname="col2"> Strängbeskrivning för felet. Vanligtvis mediets URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_URL </span> </td> 
   <td colname="col2"> Mediets URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_TYPE </span> </td> 
   <td colname="col2"> Medietyp (HLS). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RESOURCE_ID </span> </td> 
   <td colname="col2"> Medie-ID. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK tar emot dessa felkoder och strängar från videomotorn.

>[!IMPORTANT]
>
>En fullständig lista över Adobe Primetime DRM-klientfelkoder finns på [Felmeddelandereferens för DRM-klient](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).
