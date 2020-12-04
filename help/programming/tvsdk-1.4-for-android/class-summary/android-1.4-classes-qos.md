---
description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-title: QoS-klasser
title: QoS-klasser
uuid: c1f0218d-4a79-4141-9a74-e70ac4f70aa5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# QoS-klasser {#qos-classes}

Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.

Paket: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html) Paket: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Namn </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">mätvärden.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span></td> 
   <td colname="2"> Innehåller information om hur mycket tid spelaren tillbringade med buffring och hur ofta en buffringshändelse inträffade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a> </span></td> 
   <td colname="2">Anger information om plattformen och operativsystemet som frasen
    kör: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Version av plattformens operativsystem </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Versionsnummer för frasbiblioteket </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Enhetens modellnamn </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Namn på enhetstillverkare </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">Enhetens UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Skärmens bredd/höjd </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> Innehåller olika QoS-information om inläsning av olika resurser (filer, manifest eller spellista, fragment/segment, spår och så vidare). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> PlaybackInformation</a></span> </td> 
   <td colname="2"> Innehåller information om hur uppspelningen fungerar. Detta inkluderar bildrutehastighet, profilens bithastighet, den totala buffringstiden, antalet buffringsförsök, den tid det tog att hämta den första byten från det första videobildfragmentet, den tid det tog att återge den första bildrutan, den buffertlängd som för tillfället används och bufferttiden. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">mätvärden.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Anger hur lång tid det tog för mediet att läsas in, hur mycket det tog för spelaren att återge den första bildrutan eller, om ett fel inträffar, att misslyckas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">mätvärden.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackMetrics</a> </span></td> 
   <td colname="2"> Anger information om hur uppspelningen fungerar. Detta inkluderar bildrutehastighet, bithastighet, buffertlängd och så vidare. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">mätvärden.<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Anger hur många sekunder spelaren tillbringade och hur mycket tid videon faktiskt spelades upp på skärmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">Tillhandahåller viktiga QoS-mått för både uppspelning och enheten. Providerklass för QOS-information.</td> 
  </tr> 
 </tbody> 
</table>
