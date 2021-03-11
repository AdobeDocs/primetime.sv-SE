---
description: Den här tabellen visar detaljerad information om WARN-typmeddelanden.
title: Varningsmeddelandekoder
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---


# Varningsmeddelandekoder {#warning-notification-codes}

Den här tabellen visar detaljerad information om WARN-typmeddelanden.

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
   <td colname="1"><span class="codeph"> 200000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR  </span><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> <p>En uppspelningsrelaterad åtgärd misslyckades, men uppspelningen kan fortsätta. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Annonslösningar</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> RESOURCE_PLACEMENT_ MISSLYCKADES  </span><span class="codeph"> AD_RESOLVER_METADATA_INVALID  </span> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Annonslösaren kunde inte matcha/infoga annonsinnehållet. Uppspelningen kan fortsätta. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET, INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>Ett fel uppstod vid försök att läsa in en annons. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> INTERNT_FEL, AD_ID,BESKRIVNING</span> </td> 
   <td colname="5"> <p>Det gick inte att matcha annonsen på grund av en ogiltig VAST-URL eller på grund av att ingen annons returnerades från VAST-adaptern. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Bakgrundsmanifest</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000  </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_VARNING</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> ERRORBACKGROUND_MANIFEST_WARNING_</span> <span class="codeph"> NAMEDESCRIPTION</span> </td> 
   <td colname="5"> <p> Fel vid hämtning av bakgrundsmanifest. Alla problem med att uppdatera bakgrundsmanifestet skickas som en TVSDK-varning och orsakar inte att uppspelningen avbryts. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001  </span> </td> 
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
   <td colname="1" morerows="1"><span class="codeph"> 209100  </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING  </span> </td> 
   <td colname="3" morerows="1"> <p>Ingen </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> NATIVE_ERROR_NAME  </span><span class="codeph"> DESCRIPTION  </span> </p> </td> 
   <td colname="5"> <p>Ett fel uppstod i AVE-biblioteket på låg nivå. </p> <p>Information om NATIVE_ERROR-meddelanden</a> finns i <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Information om värdena för dessa metadatafält. </a></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_</span> <span class="codeph"> CODEDRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> DRM-felkod och DRM-serverfelsträng. Information om NATIVE_ERROR-meddelanden</a> finns i <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Information om värdena för dessa metadatafält.</a></td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000  </span> </td> 
   <td colname="2"><span class="codeph"> UNDEFINED_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Annonssignaleringsläget definieras som anpassade intervall, men det finns inga definierade intervall. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001  </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_RANGES  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> <p> Ett eller flera tidsintervall är ogiltiga och kommer att ignoreras eller ändras. </p> <p> BESKRIVNING är en sträng som innehåller en beskrivning av de ogiltiga intervallen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Trick-läge</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000  </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> <p> Frekvensändringen misslyckades. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Allmän</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_VARNING  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Markerar en allmän varningshändelse. Inte utfärdat av TVSDK. Det är bara en markör för slutet av det numeriska kodsintervall som motsvarar varningshändelser. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[OBS!] adID och källa (URL) kan hämtas via PTAdAsset i meddelandemetadata med  `AD_ASSET` nyckeln.
