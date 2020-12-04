---
description: Den här tabellen innehåller detaljerad information om meddelanden om ERROR-typer.
seo-description: Den här tabellen innehåller detaljerad information om meddelanden om ERROR-typer.
seo-title: FELMEDDELANDEkoder
title: FELMEDDELANDEkoder
uuid: cc21473d-924e-475d-96ea-352233f664ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---


# FELMEDDELANDEkoder{#error-notification-codes}

Den här tabellen innehåller detaljerad information om meddelanden om ERROR-typer.

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

De flesta fel innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> Ett fel uppstod vid hämtning av ett fragment eller segment (både video och ljud). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> Ett fel uppstod när en sökåtgärd utfördes. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> Ett fel uppstod när en paus skulle utföras. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när information om en innehållsperiod hämtades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när uppspelningspositionen skulle hämtas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Det uppstod ett fel när QOS-informationen skulle hämtas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> Det uppstod ett fel när data skulle hämtas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Ogiltig resurs</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNINGSRESURS  </span><span class="codeph">   </span> </td> 
   <td colname="5"> Ett fel uppstod när ett resursobjekt lästes in. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_ MISSLYCKADES  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> Ett fel uppstod när en resurs placerades på tidslinjen för uppspelningen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Annonshantering</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE  </span> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Ingen </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> Det gick inte att matcha annonsen på grund av ett ogiltigt annonsmetadataformat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> Det gick inte att matcha annonser med plugin-programmet för annonser. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> Ad resolving phase has failed. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Inbyggt</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE  </span> <span class="codeph"> NATIVE_ERROR_NAME  </span> <span class="codeph"> DESCRIPTION  </span> <span class="codeph"> DESCRIPTION</span> <p><b>DRM-information:</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGNATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>Ett fel uppstod i AVE-biblioteket på låg nivå. </p> <p>Information om NATIVE_ERROR-meddelanden</a> finns i <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> Information om värdena för dessa metadatanycklar. </a></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när lågnivåbiblioteket AVE instansierades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när lågnivåbiblioteket AVE frigjordes. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när GPU-resurserna som används av AVE-biblioteket frigjordes. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod när AVE-biblioteket återställdes. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> Ett fel uppstod när en vy bifogades till AVE-biblioteket. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Konfiguration</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000  </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNINGSVOLYM  </span> </td> 
   <td colname="5"> Ett fel uppstod när volymnivån skulle anges. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Ett fel uppstod vid försök att ändra buffringsparametrarna. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> Ett fel uppstod när CC-spåren skulle visas igen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> Ett fel uppstod vid försök att ändra formateringsalternativen för CC-spåren. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004  </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span> </td> 
   <td colname="5"> Ett fel uppstod vid försök att ändra ABR-kontrollparametrar. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING  </span><span class="codeph"> INITIAL_BUFFER_TIME  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> Ett fel uppstod vid försök att ändra parametrarna för buffringskontrollen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Alternativt ljud</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> Ett fel relaterat till ett ljudspår uppstod. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Allmän</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Markerar en allmän felhändelse. Inte utfärdat av TVSDK. Detta är bara en markör för slutet av det numeriska kodsintervall som motsvarar TVSDK-felhändelser. </td> 
  </tr> 
 </tbody> 
</table>

