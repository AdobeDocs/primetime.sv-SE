---
description: Versionen av EXT-X-VERSION i .m3u8-filen påverkar vilka funktioner som är tillgängliga för programmet och vilka EXT-taggar som är giltiga i din spellista/ditt manifest.
title: Krav för EXT-X-VERSION
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Krav för EXT-X-VERSION{#ext-x-version-requirements}

Versionen av #EXT-X-VERSION i .m3u8-filen påverkar vilka funktioner som är tillgängliga för ditt program och vilka EXT-taggar som är giltiga i din spellista/ditt manifest.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Här är lite information om taggen `#EXT-X-VERSION` som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå.

   Mer information finns i [Specifikation för HTTP-direktuppspelning ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) .
* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå.

   Mer information finns i [Specifikation för HTTP-direktuppspelning](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) .
* Adobe rekommenderar att du använder minst version 2 för uppspelning på -baserade klienter.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> Attributet IV för taggen <span class="codeph"> EXT-X-KEY </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Längdvärden för flyttalets <span class="codeph"> EXTINF </span> <p>Varaktighetstaggar ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. Version 3 och senare kräver att varaktigheten är exakt i flyttal. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">Taggen <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">Taggen <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">Taggen <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">Taggen <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">The <span class="codeph"> LJUD </span> och <span class="codeph"> VIDEO </span> attribut för <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">alternativt ljud för TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
