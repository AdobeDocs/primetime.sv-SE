---
description: Tabellen innehåller detaljerad information om INFO. typmeddelanden.
seo-description: Tabellen innehåller detaljerad information om INFO. typmeddelanden.
seo-title: INFO-meddelandekoder
title: INFO-meddelandekoder
uuid: 2b9f9328-4e09-44b7-8ea5-237c46e65e73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 4%

---


# INFO-meddelandekoder{#info-notification-codes}

Tabellen innehåller detaljerad information om INFO. typmeddelanden.

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

De flesta informationsmeddelanden innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Code </th> 
   <th colname="2" class="entry"> Namn </th> 
   <th colname="3" class="entry"> Inre meddelande </th> 
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
   <td colname="1"><span class="codeph"> 300000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Uppspelningen har startat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Uppspelningen har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> En sökåtgärd initierades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> En sökåtgärd har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE  </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <span class="codeph"> CONTENT_</span> <span class="codeph"> IDCURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> Den aktuella uppspelningstiden har passerat gränsen mellan huvudinnehållet och det alternativa innehållet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE  </span> </td> 
   <td colname="3"> <p>FELMEDDELANDE. </p> </td> 
   <td colname="4"><span class="codeph"> LÄGE  </span> </td> 
   <td colname="5"> Spelarläget har ändrats. När tillståndet är FEL är det inre meddelandeobjektet det felmeddelandeobjekt som utlöste växlingen till FELläge. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_MARKER  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> Innehållsmarkören har tagits emot. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100  </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_</span> <span class="codeph"> URLFRAGMENT_</span> <span class="codeph"> SIZEFRAGMENT_DOWNLOAD_</span> <span class="codeph"> DURATIONPERIOD_INDEX</span> </td> 
   <td colname="5"> Anger information om hur videosegment hämtas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101  </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> HÖJD</span> <p><span class="codeph"> BREDD</span> </p> </td> 
   <td colname="5"> Storleken på videouppspelningsfönstret har ändrats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Adaptiva bithastigheter (ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000  </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE  </span><span class="codeph"> CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> Videons bithastighet ändrad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Annonshantering</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000  </span> </td> 
   <td colname="2"><span class="codeph"> TIMELINE_CHANGE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span><span class="codeph"> PERIOD_INDEX  </span> </td> 
   <td colname="5"> Tidslinjen har ändrats (alternativt innehåll har till exempel lagts till eller tagits bort). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_PLACEMENT_COMPLETE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> PROPOSED_AD_</span> <span class="codeph"> BREAKACCEPTED_AD_BREAK</span> </td> 
   <td colname="5"> En föreslagen annonsbrytning accepterades av <code>primetime-sdk-name</code> och placerades (helt eller bara delvis) på tidslinjen för uppspelningen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK  </span> </td> 
   <td colname="5"> Uppspelningen av en viss annonsbrytning har startat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK  </span> </td> 
   <td colname="5"> Uppspelningen av en viss annonsbrytning har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004  </span> </td> 
   <td colname="2"><span class="codeph"> AD_START  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> </td> 
   <td colname="5"> Uppspelningen av en viss annons har startat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> </td> 
   <td colname="5"> Uppspelningen av en viss annons har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006  </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> FÖRLOPP</span> </td> 
   <td colname="5"> Uppspelningen av en viss annons har nått en viss procentandel av den annonsen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007  </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> TYP</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> NAMN</span> <p><span class="codeph"> TID</span> </p> </td> 
   <td colname="5"> En ny tidsbestämd metadata upptäcktes i manifestet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008  </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Returnerar information om en annons som användaren klickade på. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_SKIPPED</span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> AD</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> Ett annonsavbrott hoppades över. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>LBA (Late-binding audio)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID  </span><span class="codeph"> CURRENT_MEDIA_TIME  </span> </td> 
   <td colname="5"> Ljudspåret har ändrats. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000  </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP  </span> </td> 
   <td colname="5"> Nya DRM-data är tillgängliga. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Allmän</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO  </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Markerar en allmän informationshändelse. Inte utfärdat av TVSDK. Det är bara en markör för slutet av det numeriska kodsintervall som motsvarar TVSDK-informationshändelser. </p> </td> 
  </tr> 
 </tbody> 
</table>

