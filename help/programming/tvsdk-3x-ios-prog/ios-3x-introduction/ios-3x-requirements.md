---
description: TVSDK har särskilda krav för medieinnehåll, manifestinnehåll, DRM och programvaruversioner.
title: Krav
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Krav {#requirements}

TVSDK kräver specifika egenskaper för mediainnehåll, manifestinnehåll, DRM och programversioner.

## System- och programvarukrav {#section_96E5B079900246E78682AE44D3F23068}

Om du vill använda TVSDK måste du se till att maskinvaran, operativsystemet och programversionerna uppfyller minimikraven nedan.

| Operativsystem | iOS 7.0 eller senare |
|---|---|
| Xcode | Xcode 10 för iOS 12 och Xcode 9 för iOS 11 |

## Innehåll och manifestkrav {#section_72DD0E4DA9774DCCADB42887497F1386}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Nyckelbildrutor för innehållssegment | Varje innehållssegment måste börja med en nyckelbildruta. |
|---|---|
| Sekvensnummer i live/linjär video | Måste matcha alla bithastighetsåtergivningar för huvudinnehållet vid en viss tidpunkt. |

## Krav för EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

Versionen av `#EXT-X-VERSION` i [!DNL .m3u8] manifestfilen påverkar vilka funktioner som är tillgängliga för ditt program och vilka taggar som `EXT` är giltiga.

Här är lite information om taggen `#EXT-X-VERSION` , som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå. Mer information finns i Specifikation](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) för [HTTP-liveströmning.
* Adobe rekommenderar att du använder minst version 2 av HLS för uppspelning i TVSDK-baserade klienter.

  Klienter och servrar måste implementera versionerna på följande sätt:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Använd minst den här versionen </th> 
   <th colname="2" class="entry"> Så här använder du funktionerna </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> IV-attributet för EXT-X-KEY-taggen <span class="codeph"> </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Flyttal <span class="codeph"> EXTINF-varaktighetsvärden </span> <p>Varaktighetstaggarna ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. &lt;/title&gt;&lt;/duration&gt; Version 3 och senare kräver att varaktigheter anges exakt, i flyttal. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Taggen <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Taggen <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">The <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">The <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">The <span class="codeph"> LJUD </span> och <span class="codeph"> VIDEO </span> attributen för <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">alternativt ljud för TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
