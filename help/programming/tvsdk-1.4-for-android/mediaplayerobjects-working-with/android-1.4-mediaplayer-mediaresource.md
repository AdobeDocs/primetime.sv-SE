---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
title: MediaPlayer-metoder för åtkomst till MediaResource-information
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# MediaPlayer-metoder för åtkomst till MediaResource-information{#mediaplayer-methods-for-accessing-mediaresource-information}

Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Metod </th> 
   <th colname="3" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Annonstaggar</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Listget&lt;string&gt; AdTags()  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med annonstaggar som används för annonsplaceringsprocessen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Liveström</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk isLive();  </span> </td> 
   <td colname="3"> <p>True om strömmen är live; false om det är VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM-skyddad</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk isProtected();  </span> </td> 
   <td colname="3"> <p>True om strömmen är DRM-skyddad. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;drmmetadatainfo&gt; DRMMetadataInfos();  </span> </td> 
   <td colname="3"> <p>Visar alla DRM-metadataobjekt som identifieras i manifestet. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Undertexter</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk hasClosedCaptions();  </span> </td> 
   <td colname="3"> <p>True om det finns spår för undertextning. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;closedcaptionstrack&gt; ClosedCationsTracks();  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga spår för undertextning. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> <p>Hämtar det aktuella textningsspåret som är markerat med <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>Anger att ett undertextningsspår ska vara det aktuella undertextningsspåret. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Alternativa ljudspår</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleskt hasAlternateAudio();  </span> </td> 
   <td colname="3"> <p>True om strömmen har alternativa ljudspår. </p> <p>Tips:  Huvudljudspåret (standardljudspåret) är också en del av den alternativa ljudspårslistan. </p> <p>TVSDK för Android betraktar huvudljudspåret som ett av objekten i den alternativa ljudspårslistan. Därför är det enda fallet där <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> returnerar false när strömmen inte har något ljud alls. Om innehållet bara har ett ljudspår returnerar metoden true och <span class="codeph"> MediaPlayerItem.getAudioTracks </span> returnerar en lista med ett enda element (standardljudspåret). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;audiotrack&gt; AudioTracks();  </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga alternativa ljudspår. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;audiotrack&gt; AudioTracks();  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga alternativa ljudspår. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> <p>Hämtar det ljudspår som valts med <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack )  </span> </td> 
   <td colname="3"> <p>Väljer att ett ljudspår ska vara aktuellt ljudspår. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Tidsbestämda metadata</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> <p>True if the stream has associated timed metadata. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;timedmetadata&gt; TimedMetadata();  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tidsbestämda metadataobjekt som är associerade med strömmen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> <p>True if the stream is a multiple bit rate (MBR) stream. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;profile&gt; Profiles();  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med associerade bithastighetsprofiler. För varje profil kan du hämta dess bithastighet och profilens höjd och bredd. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Trick play</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleskt isTrickPlaySupported();  </span> </td> 
   <td colname="3"> <p>True if the player supports fast forward, rewind, and resume. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListAvailablePlaybackRates  </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga uppspelningsfrekvenser i samband med trippelfunktionen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Medieresurs</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> <p>Returnerar den medieresurs som är associerad med det här objektet. </p> </td> 
  </tr> 
 </tbody> 
</table>

