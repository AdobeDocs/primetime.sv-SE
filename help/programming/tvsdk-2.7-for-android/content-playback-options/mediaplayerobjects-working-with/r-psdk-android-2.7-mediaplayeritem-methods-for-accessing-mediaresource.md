---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-title: MediaPlayerItem-metoder för åtkomst av MediaResource-information
title: MediaPlayerItem-metoder för åtkomst av MediaResource-information
uuid: c6e77eb7-cefd-48aa-9373-2b44a96217a5
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# MediaPlayerItem-metoder för åtkomst av MediaResource-information {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Metod </th> 
   <th colname="3" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Annonstaggar</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;String&gt; getAdTags() </span> </td> 
   <td colname="3"> Innehåller en lista med annonstaggar som används för annonsplaceringsprocessen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Liveström</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk isLive(); </span> </td> 
   <td colname="3"> True om strömmen är live; false om det är VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM-skyddad</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk isProtected(); </span> </td> 
   <td colname="3"> True om strömmen är DRM-skyddad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;DRMMetadataInfo&gt; getDRMMetadataInfo(); </span> </td> 
   <td colname="3"> Visar alla DRM-metadataobjekt som identifieras i manifestet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Undertexter</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolesk hasClosedCaptions(); </span> </td> 
   <td colname="3"> True om det finns spår för undertextning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;ClosedCaptionsTrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga spår för undertextning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> Hämtar det aktuella textningsspåret som är markerat med <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> Anger att ett undertextningsspår ska vara det aktuella undertextningsspåret. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Alternativa ljudspår</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleskt hasAlternateAudio(); </span> </td> 
   <td colname="3"> True om strömmen har alternativa ljudspår. <p>Obs!  Huvudljudspåret (standardljudspåret) är också en del av den alternativa ljudspårslistan. </p> <p>TVSDK för Android betraktar huvudljudspåret som ett av objekten i den alternativa ljudspårslistan. Därför är det enda fallet där <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> returnerar false när strömmen inte har något ljud alls. Om innehållet bara har ett ljudspår returnerar metoden true och <span class="codeph"> MediaPlayerItem.getAudioTracks </span> returnerar en lista med ett enda element (standardljudspåret). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;AudioTrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga alternativa ljudspår. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> Hämtar det ljudspår som har valts med <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> Väljer att ett ljudspår ska vara aktuellt ljudspår. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tidsbestämda metadata</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata(); </span> </td> 
   <td colname="3"> True if the stream has associated timed metadata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;TimedMetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> Innehåller en lista med tidsbestämda metadataobjekt som är associerade med strömmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Flera profiler (bithastighet)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic(); </span> </td> 
   <td colname="3"> True if the stream is a multiple bit rate (MBR) stream. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt;Profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> Visar en lista med associerade bithastighetsprofiler. För varje profil kan du hämta dess bithastighet och profilens höjd och bredd. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Profil getSelectedProfile() </span> </td> 
   <td colname="3"> Hämtar den markerade profilen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Trick play</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleskt isTrickPlaySupported(); </span> </td> 
   <td colname="3"> True if the player supports fast forward, rewind, and resume. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga uppspelningsfrekvenser i samband med trippelfunktionen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Float getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> Hämtar den valda uppspelningshastigheten. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> Returnerar den <span class="codeph"> MediaPlayerItemConfig- </span> instans som är associerad med det här objektet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Medieresurs</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> Returnerar den medieresurs som är associerad med det här objektet. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> Returnerar medieidentifieraren som är associerad med det här objektet. Detta ID anges när objektet läses in med <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
