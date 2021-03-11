---
description: TVSDK kräver specifika egenskaper för mediematerial, manifestinnehåll och programversioner.
title: Krav
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Krav {#requirements}

TVSDK kräver specifika egenskaper för mediematerial, manifestinnehåll och programversioner.

## System- och programvarukrav {#section_61C32A0209C44230B392B113B85643EE}

Om du vill använda TVSDK måste du se till att maskinvaru-, operativsystem- och programversionerna uppfyller de minimikrav som listas nedan.

Operativsystem: iOS 6.0 eller senare

## Krav för innehåll och manifest {#section_05FA02E2189742008DA09D87E66DCAB7}

Kontrollera begränsningar och krav för strömmar och spellistor (manifest), inklusive DRM-krypteringsnycklar.

| Nyckelbildrutor för innehållssegment | Varje innehållssegment måste börja med en nyckelbildruta. |
|---|---|
| Sekvensnummer i live/linjär video | Måste matcha alla bithastighetsåtergivningar för huvudinnehållet vid en given tidpunkt. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

Versionen av `#EXT-X-VERSION` i [!DNL .m3u8]-filen påverkar vilka funktioner som är tillgängliga för ditt program och vilka `EXT`-taggar som är giltiga i din spellista/ditt manifest.

Här är lite information om taggen `#EXT-X-VERSION` som anger HLS-protokollversionen:

* Versionen måste matcha funktionerna och attributen i HLS-spellistan. Annars kan uppspelningsfel uppstå.

   Mer information finns i [Specifikation för HTTP-direktuppspelning](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Om taggen inte finns med i överordnad spellistor eller mediespelningslistor, eller om ingen version anges, används version 1 som standard. Innehåll som inte är kompatibelt med version 1 spelas inte upp.
* Adobe rekommenderar att du använder minst version 2 för uppspelning i TVSDK-baserade klienter.

Klienter och servrar måste implementera versionerna på följande sätt:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Använd åtminstone den här versionen </th> 
   <th colname="2" class="entry"> Så här använder du funktionerna </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> Attributet IV för taggen <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Flyttalsvärden <span class="codeph"> EXTINF </span> <p>Varaktighetstaggarna ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) i version 2 avrundades till heltalsvärden. Version 3 och senare kräver att varaktigheten är exakt i flyttal. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK-funktioner som annonsinfogning och sömlös ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">Taggen <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">Taggen <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">Taggen <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">Taggen <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34"><span class="codeph">-LJUDET </span> och <span class="codeph"> VIDEO </span>-attributen för <span class="codeph"> EXT-X-STREAM-INF </span>-taggen </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> alternativt ljud för TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
