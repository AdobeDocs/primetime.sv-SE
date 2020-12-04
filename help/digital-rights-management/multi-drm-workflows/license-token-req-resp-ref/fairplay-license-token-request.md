---
description: Licenstoken för FairPlay ger produktions- och testtjänster.
seo-description: Licenstoken för FairPlay ger produktions- och testtjänster.
seo-title: FairPlay-licenstokenbegäran/svar
title: FairPlay-licenstokenbegäran/svar
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 5%

---


# FairPlay-licenstokenbegäran och -svar {#fairplay-license-token-request-response}

Licenstoken för FairPlay ger produktions- och testtjänster. Denna begäran returnerar en token som kan lösas in för en FairPlay-licens.

**Metod: GET, POST** (med en www-url-encoded body som innehåller parametrar för båda metoderna)

**URL:er:**

* **Produktion:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Test:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Exempelbegäran:**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **Exempelsvar:**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**Frågeparametrar för begäran**

**Tabell 3: Parametrar för tokenfråga**

| Frågeparameter | Beskrivning | Obligatoriskt? |
|--- |--- |--- |
| customerAuthenticator Customer authenticator as query parameter customerAuthenticator FairPlay | Det här är er API-nyckel för era kunder, en för era produktions- och testmiljöer. Det finns på fliken Admin Dashboard för ExpressPlay. | Ja |
| errorFormat | Antingen html eller json. Om html (standard) anges en HTML-representation av eventuella fel i svarets entitetstext. Om json anges returneras ett strukturerat svar i JSON-format. Mer information finns i [JSON-fel](https://www.expressplay.com/developer/restapi/#json-errors). MIME-typen för svaret är antingen text/uri-list on success, text/html for HTML error format eller application/json for JSON error format. | Nej |

**Tabell 4: Parametrar för licensfråga**

| **Frågeparameter** | **Beskrivning** | **Obligatoriskt?** |
|---|---|---|
| `generalFlags` | En hexadecimal sträng på 4 byte som representerar licensflaggorna. &quot;0000&quot; är det enda tillåtna värdet. | Nej |
| `kek` | Nyckelkrypteringsnyckel (KEK). Tangenter lagras krypterade med en KEK med hjälp av en nyckelomslutningsalgoritm (AES Key Wrap, RFC3394). Om `kek` anges måste antingen en av `kid`- eller `ek`-parametrarna anges, *men inte båda*. | Nej |
| `kid` | En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln eller en sträng `'^somestring'`. Längden på strängen följt av `'^'` får inte vara längre än 64 tecken. | Nej |
| `ek` | En hexadecimal strängrepresentation av den krypterade innehållsnyckeln. | Nej |
| `contentKey` | En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln | Ja, såvida inte `kek` och `ek` eller `kid` anges. |
| `iv` | En 16 byte hexadecimal strängbeteckning för innehållskryptering IV | Ja |
| `rentalDuration` | Hyrningens varaktighet i sekunder (standard - 0) | Nej |
| `fpExtension` | Ett kort formulär som omsluter `extensionType` och `extensionPayload`, som en kommaavgränsad sträng. Exempel: […] `&fpExtension=wudo,AAAAAA==&`[…] | Nej, vilket tal som helst kan användas |

**Tabell 5: Frågeparametrar för tokenbegränsning**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Frågeparameter</b> </th> 
   <th class="entry"> <b>Beskrivning</b> </th> 
   <th class="entry"> <b>Obligatoriskt?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime  </span> </td> 
   <td> Förfallotid för denna token. Detta värde MÅSTE vara en sträng i <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 339 </a> datum-/tidsformat i zondesignern för Z ("Zulu time") eller ett heltal föregånget av tecknet "+". Ett exempel på ett RFC 3339-datum/tid är <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>Om värdet är en sträng i <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 339 </a> datum-/tidsformat representerar det ett absolut förfallodatum/tid för token. Om värdet är ett heltal som föregås av ett plustecken tolkas det som ett relativt antal sekunder, från utgivningen, att token är giltig. </p> <span class="codeph"> +60 </span> anger till exempel en minut. Maximal token- och standardtokenlivstid (om inget anges) är 30 dagar. </td> 
   <td> Nej </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 6: Parametrar för korrelationsfråga**

| **Frågeparameter** | **Beskrivning** | **Obligatoriskt?** |
|---|---|---|
| `cookie` | En godtycklig sträng som är upp till 32 tecken lång och som finns i token och loggas av tokeninlösenservern. Detta kan användas för att korrelera loggposter på inlösenservern och poster på tjänsteleverantörens servrar. | Nej |

**Svar**

**Tabell 7: HTTP-svar**

| **HTTP-statuskod** | **Beskrivning** | **Content-Type** | **Entitetstexten innehåller** |
|---|---|---|---|
| `200 OK` | Inget fel. | `text/uri-list` | URL för hämtning av licens + token |
| `400 Bad Request` | Ogiltiga argument | `text/html` eller  `application/json` | Felbeskrivning |
| `401 Unauthorized` | Autentisering misslyckades | `text/html` eller  `application/json` | Felbeskrivning |
| `404 Not found` | Felaktig URL | `text/html` eller  `application/json` | Felbeskrivning |
| `50x Server Error` | Serverfel | `text/html` eller  `application/json` | Felbeskrivning |

**Tabell 8: Felkoder för händelse**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Code</b> </th> 
   <th class="entry"> <b>Beskrivning</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Ogiltig förfallotid för token: &lt;information&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Ogiltig IP-adress </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Ogiltig krypteringsnyckel för innehåll: &lt;information&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Ogiltiga utdatakontrollflaggor har angetts: &lt;information&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Autentiseringstoken måste anges </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Ogiltig autentiseringstoken: &lt;information&gt; <p>Obs!  Detta kan inträffa om autentiseraren är fel eller när testnings-API:t på <span class="filepath"> *.test.expressplay.com </span> används med produktionsautentiseraren och vice versa. </p> <p importance="high">Obs!  Test SDK och Advanced Test Tool (ATT) fungerar bara med <span class="filepath"> *.test.expressplay.com </span>, medan produktionsenheter måste använda <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Otillräckliga tokens är tillgängliga </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Rättighetstyp saknas </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Ogiltig rättighetstyp </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Sluttid för uthyrningsperiod saknas </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Speltid för saknad uthyrning </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Ogiltig varaktighet för uthyrning av uppspelning </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> Innehållskrypteringsnyckeln måste vara 32-hexadecimala siffror lång </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay Admin-fel: &lt;information&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Tjänstkonto inaktiverat </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Ogiltig cookie </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Ogiltig utdatakontroll, värden utanför angivet intervall </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> Inget motsvarande värde har angetts </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> Tilläggstypen ska vara 4 tecken </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> Tilläggsnyttolasten ska vara Base64-kodad </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag  </span> måste koda 4 byte </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Ett ogiltigt felformat har angetts: &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> Enheten kunde inte autentiseras </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Ogiltig token </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Saknat Kid </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Det gick inte att hämta innehållsnyckeln från nyckellagringstjänsten </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> child  </span> måste vara 32 hexadecimala tecken långa </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> barn  </span> måste vara 64 tecken långt efter ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Ogiltig <span class="codeph">-grabb </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Ogiltig krypterad nyckel eller <span class="codeph">-nyckel </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Ogiltiga allmänna flaggor </td> 
  </tr> 
  <tr> 
   <td> -6001 </td> 
   <td> Ogiltiga <span class="codeph"> FPExtension </span>-parametrar har angetts </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Ogiltig FP-tokentyp </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Ogiltig <span class="codeph"> iv </span>-parameter har angetts </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Det gick inte att generera CKC för FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Ogiltiga nyckeldata har angetts </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Tjänsten är inte auktoriserad för FairPlay-stöd </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Ogiltig uthyrningstid har angetts </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> Device ID-bindning stöds inte för FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> Alternativet FairPlay är inaktiverat </td> 
  </tr> 
 </tbody> 
</table>