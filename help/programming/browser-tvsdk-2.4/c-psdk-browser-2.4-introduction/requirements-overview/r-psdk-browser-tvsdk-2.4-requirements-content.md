---
description: Kontrollera begränsningar och krav för strömmar och spellistor (manifest).
title: Krav för innehåll och manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Krav för innehåll och manifest{#content-and-manifest-requirements}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Innehållssegmentets längd </td> 
   <td colname="col2"> Ett segments varaktighet får inte överskrida den målvaraktighet som anges i manifestfilen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Innehållskrav </td> 
   <td colname="col2"> Alla TS-segment ska börja med en nyckelbildruta. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS-innehåll </td> 
   <td colname="col2"> <p>Kom ihåg följande: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">AAC-SSR-ljud stöds inte. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">Ljudkodekar AC3 och Enhanced AC3 stöds inte. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">HLS-strömmar med avbrott, men inga kontinuitetsmarkörer stöds inte. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live stöder inte tidsstämpelrollover. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Ads in the DVR window of HLS Live streams are not resolved. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">Byteintervallet stöds inte med AES-128-krypterat innehåll. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> DASH-innehåll </td> 
   <td colname="col2"> <p>Kom ihåg följande: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">För Live-strömmar - Live-profilen med dynamisk typ stöds. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">För VOD-strömmar - live-profilen med statisk typ stöds. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">För VOD-strömmar - On-demand-profilen är inte certifierad för annonsarbetsflöden. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">Uppspelning av DASH-strömmar med flera punkter stöds inte. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">Inbäddade bildtexter (608/708), som signaleras via taggen Accessibility, stöds. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">Fragmenterade/segmenterade VTT-filer stöds inte. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">Strömmar med anpassade inband-taggar är inte certifierade. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>

