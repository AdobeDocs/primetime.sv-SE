---
description: Du kan använda Primetime Player-API:t för att anpassa spelarens beteende.
title: Mediacore-klasser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Mediacore-klasser {#mediacore-classes}

Du kan använda Primetime Player-API:t för att anpassa spelarens beteende.

Om du vill se den fullständiga API-dokumentationen för TVSDK går du till [Adobe Primetime API-referenser](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

Dessa klasser beskriver din mediespelare och dess resurser.
Paket: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>Namn </p> </th> 
   <th colname="2" class="entry"> <p>Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> </a>  ABRControlParametersABRControlParameters</span> </td> 
   <td colname="2"> En klass som kapslar in alla adaptiva parametrar för bithastighetskontroll. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdClientFactory.html" format="html" scope="external"> AdClientFactory</a> </span> </td> 
   <td colname="2"> Gränssnitt för att skapa affärsmöjlighetsdetektorer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdvertisingFactory.html" format="html" scope="external"> AdvertisingFactory</a> </span> </td> 
   <td colname="2"> Factory-klass som tillåter anpassning av annonsbeslutsprocessen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a> </span> </td> 
   <td colname="2"> En klass som kapslar in alla parametrar för buffertkontroll. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> Standardimplementering för annonsuppspelningsbeteenden. Gränssnitt som gör att program kan anpassa annonsbeteenden.</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2">Standardklassimplementering av gränssnittet <span class="codeph"> MediaPlayer</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a> </span> </td> 
   <td colname="2">Offentligt gränssnitt för klassen <span class="codeph"> DefaultMediaPlayer</span>. Innehåller uppräkningar för Event, PlayerState och Visibility. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html" format="html" scope="external"> MediaPlayer.AdPlaybackEventListener</a></span> </td> 
   <td colname="2"> Gränssnittsdefinition för en uppsättning återanrop som ska anropas under annonsuppspelning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html" format="html" scope="external"> MediaPlayer.DRMEventListener</a></span> </td> 
   <td colname="2"> Gränssnittsdefinition för ett återanrop som ska anropas när skyddade metadata blir tillgängliga. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.EventListener.html" format="html" scope="external"> MediaPlayer.EventListener</a> </span> </td> 
   <td colname="2"> Det markörgränssnitt som används för att sammanföra registrering av händelseavlyssnare. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html" format="html" scope="external"> MediaPlayer.PlaybackEventListener</a> </span> </td>
   <td colname="2"> Gränssnittsdefinition för en uppsättning återanrop som ska anropas under uppspelning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html" format="html" scope="external"> MediaPlayer.QOSEventListener</a> </span> </td> 
   <td colname="2"> Gränssnittsdefinition för en uppsättning återanrop som ska anropas under QoS. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a> </span> </td> 
   <td colname="2"> Gränssnitt som representerar ljud-video-media. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a> </span> </td> 
   <td colname="2"> En klass som läser in en mediespelarresurs och skapar motsvarande MediaPlayerItem-objekt. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html" format="html" scope="external"> MediaPlayerItemLoader.LoaderListener</a> </span> </td> 
   <td colname="2"> Gränssnitt som definierar de avlyssnarmetoder som är associerade med MediaPlayerItemLoader-objektet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a> </span> </td> 
   <td colname="2"> Klass för den vy som ska användas av MediaPlayer för videoåtergivning. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a> </span> </td> 
   <td colname="2"> En klass som omsluter all information om en medieresurs. Inkluderar uppräkning för medieresurstypen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PlacementOpportunityDetector.html" format="html" scope="external"> PlacementOpportunityDetector</a> </span> </td> 
   <td colname="2"> Gränssnitt som används för att bearbeta in-manifest-referenser som ska användas som placeringar för annonsbeslutsprocessen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a> </span> </td> 
   <td colname="2"> En klass som kapslar in de anpassade taggar som används av mediespelaren när annonsplaceringen utförs, förutom standardreferenstaggarna. Den innehåller även de taggnamn som programmet vill bli informerad om. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> TextFormat</a> </span> </td> 
   <td colname="2"> Gränssnitt som kapslar in olika attribut som beskriver ett textformat (t.ex. formatet för undertexter). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormatBuilder.html" format="html" scope="external"> TextFormatBuilder</a></span> </td> 
   <td colname="2"> Klassmetoder för att ange textformatering. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> Version</a></span> </td> 
   <td colname="2"> En klass som innehåller version och beskrivning av TVSDK. </td> 
  </tr> 
 </tbody> 
</table>
