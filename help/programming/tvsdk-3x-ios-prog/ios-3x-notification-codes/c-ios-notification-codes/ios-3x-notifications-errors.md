---
description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-description: TVSDK-meddelandesystemet genererar olika fel-, varnings- och informationsmeddelanden som tillhandahåller diagnostiska metadata.
seo-title: 'null'
title: 'null'
uuid: 20828188-817a-471c-acbc-aeb5f336356b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# FELMEDDELANDEkoder {#error-notification-codes}

Den här tabellen innehåller detaljerad information om meddelanden om ERROR-typer.

De flesta fel innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Code</b></th> 
   <th colname="2" class="entry"><b>Namn</b></th> 
   <th colname="3" class="entry"><b>InnerNotification</b></th> 
   <th colname="4" class="entry"><b>Metadatanycklar</b></th> 
   <th colname="5" class="entry"><b>Kommentarer</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE - </span><span class="codeph"> BESKRIVNING </span> </td> 
   <td colname="5"></td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Uppspelning</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span><span class="codeph"> INTERNAL_ERROR- </span><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="5"> <p>Ett fel uppstod när en sökåtgärd utfördes. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Ett fel uppstod när en paus skulle utföras. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Ogiltig resurs</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Annonshantering</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Det gick inte att matcha annonsen på grund av ett ogiltigt annonsmetadataformat. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Ad resolving phase has failed. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Inbyggt</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Ett iOS-fel på låg nivå inträffade. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Konfiguration</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Ett fel uppstod när CC-spåren skulle visas igen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR </span> </td> 
   <td colname="3"> <span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Ett fel uppstod vid försök att ändra formateringsalternativen för CC-spåren. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS-unik</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_INCOMPATIBLE </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>HLS-versionen av annonserna är högre än HLS-versionen av innehållet. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001 </span> </td> 
   <td colname="2"><span class="codeph"> ARGUMENT_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Argumentfel </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002 </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span> </td> 
   <td colname="5"> <p>Det gick inte att parsa m3u8. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003 </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Det gick inte att parsa WebVtt. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004 </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Segmentet överskrider angiven bandbredd för variant. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005 </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Mediesekvensnumret är inte synkroniserat på alla HLS-strömmar i denna MBR. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006 </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span><span class="codeph"> URL </span><span class="codeph"> INTERNAL_ERROR </span> </td> 
   <td colname="5"> <p>Filen saknas eller svarar inte. </p> <p>HTTP 404: Filen hittades inte. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007 </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Det gick inte att hämta annonser. Tomt svar. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Det gick inte att hämta annonser. Timeoutfel. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> <p>Ett fel uppstod när undertextningsspåret ändrades. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010 </span> </td> 
   <td colname="2"><span class="codeph"> SITECATALYST_ERROR </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> BESKRIVNING </span> </td> 
   <td colname="5"> <p>Platskatalysatorfel. Se beskrivning. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPATIBLE </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>Annonsens MÅLLÄNGD är längre än innehållets MÅLLÄNGD. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID och källa (URL) kan hämtas via `PTAdAsset` i meddelandemetadata med `AD_ASSET` nyckeln.
>
>Attributet `[]` anger en valfri nyckel för meddelanden.
