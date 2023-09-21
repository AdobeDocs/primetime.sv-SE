---
description: TVSDK kräver specifika egenskaper för medieinnehåll, manifestinnehåll och programvaruversioner.
title: Krav
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Krav {#requirements}

TVSDK kräver specifika egenskaper för mediematerial, manifestinnehåll och programversioner.

## System- och programvarukrav {#section_61C32A0209C44230B392B113B85643EE}

Om du vill använda TVSDK måste du se till att maskinvaran, operativsystemet och programversionerna uppfyller minimikraven nedan.

Operativsystem: iOS 6.0 eller senare

## Innehåll och manifestkrav {#section_05FA02E2189742008DA09D87E66DCAB7}

Kontrollera begränsningarna och kraven för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Nyckelramar för innehållssegment | Varje innehållssegment måste börja med en nyckelram. |
|---|---|
| Sekvensnummer i live/linjär video | Måste matcha alla bithastighetsåtergivningar för huvudinnehållet vid en given tidpunkt. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

Versionen av `#EXT-X-VERSION` i [!DNL .m3u8] filen påverkar vilka funktioner som är tillgängliga för programmet och vilka `EXT` -taggar är giltiga i din spellista/ditt manifest.

Här är lite information om taggen `#EXT-X-VERSION` , som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå.

  Mer information finns i Specifikation](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) för [HTTP-liveströmning.
* Om taggen inte ingår i huvud- eller mediespelningslistorna, eller om ingen version anges, används version 1 som standard. Innehåll som inte uppfyller version 1 spelas inte upp.
* Adobe rekommenderar att du använder minst version 2 för uppspelning i TVSDK-baserade klienter.

Klienter och servrar måste implementera versionerna på följande sätt:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Använd minst den här versionen </th> 
   <th colname="2" class="entry"> Så här använder du dessa funktioner </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> Attributet IV för <span class="codeph"> EXT-X-KEY </span> -tagg. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Flyttal <span class="codeph"> EXTINF-varaktighetsvärden </span> <p>Varaktighetstaggarna ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. &lt;/title&gt;&lt;/duration&gt; Version 3 och senare kräver att varaktigheter är exakta i flyttal. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK-funktioner som annonsinfogning och sömlös ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">Taggen <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">Taggen <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">The <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">The <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">The <span class="codeph"> LJUD </span> och <span class="codeph"> VIDEO </span> attributen för <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> alternativt ljud för TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
