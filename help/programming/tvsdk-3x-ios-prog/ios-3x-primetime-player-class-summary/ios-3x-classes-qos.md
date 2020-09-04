---
description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-description: Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.
seo-title: QoS-klasser
title: QoS-klasser
uuid: f145b744-6385-40df-aaee-ae9430d85895
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# QoS-klasser {#qos-classes}

Dessa klasser innehåller information som hjälper dig att avgöra hur bra spelaren fungerar.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Namn</b></th> 
   <th colname="2" class="entry"><b>Beskrivning</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
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
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> Innehåller information om hur uppspelningen fungerar. Detta inkluderar bildrutehastighet, profilens bithastighet, den totala buffringstiden, antalet buffringsförsök, den tid det tog att hämta den första byten från det första videobildfragmentet, den tid det tog att återge den första bildrutan, den buffertlängd som för tillfället används och bufferttiden. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
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