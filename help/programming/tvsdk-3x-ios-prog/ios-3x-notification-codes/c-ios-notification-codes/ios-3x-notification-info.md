---
description: Den här tabellen innehåller detaljerad information om INFO-typmeddelanden.
seo-description: Den här tabellen innehåller detaljerad information om INFO-typmeddelanden.
seo-title: INFO-meddelandekoder
title: INFO-meddelandekoder
uuid: 21297863-dac1-45a4-ac9d-309d1f746f8b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# INFO-meddelandekoder {#info-notification-codes}

Den här tabellen innehåller detaljerad information om INFO-typmeddelanden.

De flesta informationsmeddelanden innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Code</b></th> 
   <th colname="2" class="entry"><b>Namn</b></th> 
   <th colname="3" class="entry"><b>Inre meddelande</b></th> 
   <th colname="4" class="entry"><b>Metadatanycklar</b></th> 
   <th colname="5" class="entry"><b>Kommentarer</b></th> 
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
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Uppspelningen har startat. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> Ingen </td> 
   <td colname="5"> Uppspelningen har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <p> Ingen </p> </td> 
   <td colname="5"> En sökåtgärd initierades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> Ingen </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> En sökåtgärd har slutförts. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> Spelarläget har ändrats. När tillståndet är FEL är det inre meddelandeobjektet det felmeddelandeobjekt som utlöste växlingen till FELläge. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Adaptiva bithastigheter (ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"><span class="codeph"> BITRAT </span> </td> 
   <td colname="5"> Videons bithastighet ändrad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>LBA (Late-binding audio)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Ljudspåret har ändrats. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Undertexter</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>Ingen </p> </td> 
   <td colname="4"> <p>Ingen </p> </td> 
   <td colname="5"> <p>Spår för undertexter har ändrats. </p> </td> 
  </tr> 
 </tbody> 
</table>