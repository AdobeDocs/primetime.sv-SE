---
description: TVSDK har specifika krav för mediematerial, manifestinnehåll, DRM och programversioner.
seo-description: TVSDK har specifika krav för mediematerial, manifestinnehåll, DRM och programversioner.
seo-title: Krav
title: Krav
uuid: 06e61b9f-cda2-4813-8da4-fb3e0d88ad35
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Krav {#requirements}

TVSDK kräver specifika egenskaper för mediainnehåll, manifestinnehåll, DRM och programversioner.

## System- och programvarukrav {#section_96E5B079900246E78682AE44D3F23068}

Om du vill använda TVSDK måste du se till att maskinvaru-, operativsystem- och programversionerna uppfyller de minimikrav som listas nedan.

| Operativsystem | iOS 7.0 eller senare |
|---|---|
| Xcode | Xcode 10 för iOS 12 och Xcode 9 för iOS 11 |

## Krav för innehåll och manifest {#section_72DD0E4DA9774DCCADB42887497F1386}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Nyckelbildrutor för innehållssegment | Varje innehållssegment måste börja med en nyckelbildruta. |
|---|---|
| Sekvensnummer i live/linjär video | Måste matcha alla bithastighetsåtergivningar för huvudinnehållet vid en given tidpunkt. |

## EXT-X-VERSION-krav {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

Versionen av `#EXT-X-VERSION` i manifestfilen [!DNL .m3u8] påverkar vilka funktioner som är tillgängliga för programmet och vilka `EXT`-taggar som är giltiga.

Här är lite information om taggen `#EXT-X-VERSION` som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå. Mer information finns i [Specifikation för HTTP-direktuppspelning](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe rekommenderar att minst version 2 av HLS används för uppspelning i TVSDK-baserade klienter.

   Klienter och servrar måste implementera versionerna på följande sätt:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Använd åtminstone den här versionen </th> 
   <th colname="2" class="entry"> Så här använder du funktionerna </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> Attributet IV för taggen <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Flyttalsvärden <span class="codeph"> EXTINF </span> <p>Varaktighetstaggarna ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. Version 3 och senare kräver att varaktighet anges exakt, i flyttal. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Taggen <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Taggen <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">Taggen <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Taggen <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph">-LJUDET </span> och <span class="codeph"> VIDEO </span>-attributen för <span class="codeph"> EXT-X-STREAM-INF </span>-taggen </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">alternativt ljud för TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>