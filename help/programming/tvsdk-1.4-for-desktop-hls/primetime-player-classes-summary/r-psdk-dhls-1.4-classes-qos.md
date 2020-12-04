---
description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-title: QoS-klasser
title: QoS-klasser
uuid: c1192474-d183-4995-87ef-839699844b48
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# QoS-klasser {#qos-classes}

Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.

Paket: [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html) Paket: [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Namn </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span> </td> 
   <td colname="2"> Innehåller information om hur mycket tid spelaren tillbringade med buffring och hur ofta en buffringshändelse inträffade. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> DeviceInformation</a></span> </td> 
   <td colname="2">Anger information om plattformen och operativsystemet som TVSDK körs på: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Version av plattformens operativsystem </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Versionsnummer för TVSDK-biblioteket </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Enhetens modellnamn </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Namn på enhetstillverkare </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">Enhetens UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Skärmens bredd/höjd </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> LoadInformation</a></span> </td> 
   <td colname="2"> Innehåller olika QoS-information om inläsning av olika resurser (filer, manifest eller spellista, fragment/segment, spår och så vidare). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationType</a></span> </td> 
   <td colname="2"> Uppräkningsklass som visar möjliga värden för type-egenskapen i LoadInformation-objekt. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> PlaybackInformation</a></span> </td> 
   <td colname="2"> Innehåller information om hur uppspelningen fungerar. Detta inkluderar bildrutehastighet, profilens bithastighet, den totala buffringstiden, antalet buffringsförsök, den tid det tog att hämta den första byten från det första videobildfragmentet, den tid det tog att återge den första bildrutan, den buffertlängd som för tillfället används och bufferttiden. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Anger hur lång tid det tog för mediet att läsas in, hur mycket det tog för spelaren att återge den första bildrutan eller, om ett fel inträffar, att misslyckas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> PlaybackMetrics</a></span> </td> 
   <td colname="2"> Anger information om hur uppspelningen fungerar. Detta inkluderar bildrutehastighet, bithastighet, buffertlängd och så vidare. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Anger hur många sekunder spelaren tillbringade och hur mycket tid videon faktiskt spelades upp på skärmen. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
   <td colname="2">
    <pre>
      Tillhandahåller viktiga QoS-mått för både uppspelning och enheten.
    </pre>
    <pre>
      Providerklass för QOS-information.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>

