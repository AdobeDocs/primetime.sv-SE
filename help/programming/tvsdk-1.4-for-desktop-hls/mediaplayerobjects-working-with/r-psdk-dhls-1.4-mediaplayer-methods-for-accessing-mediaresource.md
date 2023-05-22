---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
title: MediaPlayer-metoder för åtkomst till MediaResource-information
exl-id: 74e453d6-233e-4146-9f63-ab6919a4ba39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
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
   <td colname="1"> <b>Liveström </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>True om strömmen är live; false om det är VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM-skyddad</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>True om strömmen är DRM-skyddad. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get drmMetadataInfos(): Vektor.&lt;drmmetadatainfo&gt;; </span> </td> 
   <td colname="3"> <p>Visar alla DRM-metadataobjekt som identifieras i manifestet. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Undertexter</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasClosedCaptions():Boolean; </span> </td> 
   <td colname="3"> <p>True om det finns spår för undertextning. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> funktionen get closedCaptionsTracks():Vector.&lt;closedcaptionstrack&gt;; </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga spår för undertextning. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>Hämtar det aktuella textningsspåret som är markerat med <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack: com.adobe.mediacore.info:ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>Anger att ett undertextningsspår ska vara det aktuella undertextningsspåret. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Alternativa ljudspår </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>True om strömmen har alternativa ljudspår. </p> <p>Tips: Huvudljudspåret (standardljudspåret) är också en del av den alternativa ljudspårslistan. </p> <p>TVSDK for Desktop HLS betraktar huvudljudspåret som ett av objekten i den alternativa ljudspårslistan. På grund av detta är det enda fallet där <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> returnerar false när strömmen inte har något ljud alls. Om innehållet bara har ett ljudspår returnerar metoden true och <span class="codeph"> hämta AudioTracks </span> returnerar en lista med ett enda element (standardljudspåret). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga alternativa ljudspår. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga alternativa ljudspår. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>Hämtar ljudspåret som valts med <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack ) </span> </td> 
   <td colname="3"> <p>Väljer att ett ljudspår ska vara aktuellt ljudspår. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Tidsbestämda metadata</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream has associated timed metadata. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get timedMetadata():Vector.&lt;timedmetadata&gt;; </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tidsbestämda metadataobjekt som är associerade med strömmen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream is a multiple bit rate (MBR) stream. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get profiles():Vector.&lt;profile&gt;; </span> </td> 
   <td colname="3"> <p>Innehåller en lista med associerade bithastighetsprofiler. För varje profil kan du hämta dess bithastighet och profilens höjd och bredd. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Trick play </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isTrickPlaySupported():Boolean; </span> </td> 
   <td colname="3"> <p>True if the player supports fast forward, rewind, and resume. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get availablePlaybackRates():Vector.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>Innehåller en lista med tillgängliga uppspelningsfrekvenser i samband med trippelfunktionen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Mediespelare </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>Returnerar den mediaspelare som är associerad med den här spelaren. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Medieresurs</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>Returnerar den medieresurs som är associerad med det här objektet. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> function get resourceId():int </span> </td> 
   <td colname="3"> <p>Returnerar medieidentifieraren som är associerad med det här objektet. </p> </td> 
  </tr> 
 </tbody> 
</table>
