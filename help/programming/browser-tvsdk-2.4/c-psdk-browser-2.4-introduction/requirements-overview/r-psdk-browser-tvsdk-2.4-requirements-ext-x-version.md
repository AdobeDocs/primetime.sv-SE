---
description: 'Versionen av #EXT-X-VERSION i .m3u8-filen påverkar vilka funktioner som är tillgängliga för ditt program och vilka EXT-taggar som är giltiga i din spellista/ditt manifest.'
title: '#EXT-X-VERSION requirements'
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# #EXT-X-VERSION requirements{#ext-x-version-requirements}

Versionen av #EXT-X-VERSION i .m3u8-filen påverkar vilka funktioner som är tillgängliga för ditt program och vilka EXT-taggar som är giltiga i din spellista/ditt manifest.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Här är lite information om taggen `#EXT-X-VERSION` som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå. Mer information finns i [Specifikation för HTTP-direktuppspelning](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe rekommenderar att du använder minst version 2 för uppspelning i webbläsarens TVSDK-baserade klienter.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Flyttalsvärden <span class="codeph"> EXTINF </span> <p>Varaktighetstaggarna ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. Version 3 och senare kräver att varaktigheten är exakt i flyttal. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Taggen <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph">-LJUDET </span> och <span class="codeph"> VIDEO </span>-attributen för <span class="codeph"> EXT-X-STREAM-INF </span>-taggen </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

