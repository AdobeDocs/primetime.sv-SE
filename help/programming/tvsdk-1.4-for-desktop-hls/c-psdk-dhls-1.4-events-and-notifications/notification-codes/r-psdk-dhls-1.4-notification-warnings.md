---
description: Tabellen visar detaljerad information om WARN. typmeddelanden.
seo-description: Tabellen visar detaljerad information om WARN. typmeddelanden.
seo-title: Varningsmeddelandekoder
title: Varningsmeddelandekoder
uuid: 1ce5be07-f5bf-443c-b907-9768633e1300
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Varningsmeddelandekoder{#warning-notification-codes}

Tabellen visar detaljerad information om WARN. typmeddelanden.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

De flesta varningar innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Code </th> 
   <th colname="2" class="entry"> Namn </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> Metadatanycklar </th> 
   <th colname="5" class="entry"> Kommentarer </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Uppspelning</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span> </td> 
   <td colname="5"> <p>En uppspelningsrelaterad åtgärd misslyckades, men uppspelningen kan fortsätta. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Annonslösningar </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ MISSLYCKADES </span><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Annonslösaren kunde inte matcha/infoga annonsinnehållet. Uppspelningen kan fortsätta. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Bakgrundsmanifest</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_VARNING</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_ERROR</span><span class="codeph"> BACKGROUND_MANIFEST_WARNING_NAME</span><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> Fel vid hämtning av bakgrundsmanifest. Alla problem med att uppdatera bakgrundsmanifestet skickas som en TVSDK-varning och orsakar inte att uppspelningen avbryts. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_WARNING</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Inbyggt</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>Ingen </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME - </span><span class="codeph"> BESKRIVNING </span> </p> </td> 
   <td colname="5"> <p>Ett fel uppstod i AVE-biblioteket på låg nivå. </p> <p>Mer information om värdena för dessa metadatafält finns i <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Information om NATIVE_ERROR-meddelanden</a> . </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span><span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">DRM-felkod och DRM-serverfelsträng. Mer information om värdena för dessa metadatafält finns i <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> Information om NATIVE_ERROR-meddelanden</a> .
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Allmän</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_VARNING </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Markerar en allmän varningshändelse. Inte utfärdat av TVSDK. Det är bara en markör för slutet av det numeriska kodsintervall som motsvarar varningshändelser. </p> </td> 
  </tr> 
 </tbody> 
</table>

