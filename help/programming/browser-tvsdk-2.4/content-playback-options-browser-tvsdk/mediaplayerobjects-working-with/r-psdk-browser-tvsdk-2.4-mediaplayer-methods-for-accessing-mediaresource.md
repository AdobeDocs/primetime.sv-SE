---
description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-description: Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.
seo-title: MediaPlayer-attribut för åtkomst till MediaResource-information
title: MediaPlayer-attribut för åtkomst till MediaResource-information
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# MediaPlayer-attribut för åtkomst till MediaResource-information{#mediaplayer-attributes-to-access-mediaresource-information}

Med metoderna i klassen MediaPlayerItem kan du hämta information om innehållsströmmen som representeras av en inläst MediaResource.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Syfte </th> 
   <th colname="2" class="entry"> Attribut </th> 
   <th colname="3" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Liveström </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> True om strömmen är live; false om det är VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Undertexter </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> True om det finns spår för undertextning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga spår för undertextning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> Hämtar det textningsspår som markerades med <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Alternativt ljud </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>True om strömmen har alternativa ljudspår. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> Innehåller en lista med tillgängliga alternativa ljudspår. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      Hämtar det markerade ljudspåret som markerades med <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Tidsbestämda metadata </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> True if the stream has associated timed metadata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> Innehåller en lista över de tidsbestämda metadataobjekt som är associerade med strömmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Flera profiler (bithastighet) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> profiler </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Tillhandahåller en lista med associerade bithastighetsprofiler som är associerade med den här strömmen. <p>Obs!  Du kan hämta bithastigheten för varje profil och höjden och bredden på profilen. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Medieresurs </td> 
   <td colname="2"> <span class="codeph"> resurs </span> </td> 
   <td colname="3"> Returnerar den medieresurs som är associerad med det här objektet. </td> 
  </tr> 
 </tbody> 
</table>

