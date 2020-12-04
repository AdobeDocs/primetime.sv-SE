---
description: Gränssnittet för globala licenstoken tillhandahåller produktions- och testtjänster.
seo-description: Gränssnittet för globala licenstoken tillhandahåller produktions- och testtjänster.
seo-title: Tokenbegäran för Widewin-licens/svar
title: Tokenbegäran för Widewin-licens/svar
uuid: a3522422-7075-49a7-bc55-137ef84ee430
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 5%

---


# Tokenbegäran för Widewin-licens / svar {#widevine-license-token-request-response}

Gränssnittet för globala licenstoken tillhandahåller produktions- och testtjänster.

Denna HTTP-begäran returnerar en token som kan lösas in för en Widewin-licens.

**Metod: GET, POST** (med en www-url-encoded body som innehåller parametrar för båda metoderna)

**URL:er:**

* **Produktion:** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Test:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Exempelbegäran:**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **Exempelsvar:**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Tabell 13: Parametrar för tokenfråga**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Frågeparameter</b> </th> 
   <th class="entry"> <b>Beskrivning</b> </th> 
   <th class="entry"> <b>Obligatoriskt?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator  </span> </td> 
   <td> <p>Det här är er API-nyckel för era kunder, en för era produktions- och testmiljöer. Det finns på fliken Admin Dashboard för ExpressPlay. </p> </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat  </span> </td> 
   <td> Antingen <span class="codeph"> html </span> eller <span class="codeph"> json </span>. <p>Om <span class="codeph"> html </span> (standard) anges en HTML-representation av eventuella fel i svarets entitetstext. Om <span class="codeph"> json </span> anges returneras ett strukturerat svar i JSON-format. Mer information finns i <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON-fel </a>. </p> <p>MIME-typen för svaret är antingen <span class="codeph"> text/uri-list </span> för lyckat resultat, <span class="codeph"> text/html </span> för <span class="codeph"> html </span> felformat eller <span class="codeph"> application/json </span> för felformatet <span class="codeph"> json </span>. </p> </td> 
   <td> Nej </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 14: Parametrar för licensfråga**

| Frågeparameter | Beskrivning | Obligatoriskt? |
|--- |--- |--- |
| `generalFlags` | En hexadecimal sträng på 4 byte som representerar licensflaggorna. &quot;0000&quot; är det enda tillåtna värdet | Nej |
| `kek` | Nyckelkrypteringsnyckel (KEK). Tangenter lagras krypterade med en KEK med hjälp av en nyckelomslutningsalgoritm (AES Key Wrap, RFC3394). | Nej |
| `kid` | En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln eller en sträng `^somestring'`. Längden på strängen följt av `^` får inte vara längre än 64 tecken. Anteckning nedan innehåller ett exempel. | Ja |
| `ek` | En hexadecimal strängrepresentation av den krypterade innehållsnyckeln. | Nej |
| `contentKey` | En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln | Ja, om inte `kek` och `ek` eller `kid` anges |
| `contentId` | Innehålls-ID | Nej |
| `securityLevel` | Tillåtna värden är 1-5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | Ja |
| `hdcpOutputControl` | Tillåtna värden är 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | Ja |
| `licenseDuration` * | Licensens varaktighet i sekunder. Om den inte anges anges det att det inte finns någon begränsning av varaktigheten. Mer information finns i anteckningen nedan. | Nej |
| `wvExtension` | Ett kort formulär som paketerar extensionType och extensionPayload, som en kommaavgränsad sträng. Se formatet nedan. Exempel: `…&wvExtension=wudo,AAAAAA==&…` | Nej, vilket tal som helst kan användas |

Om `licenseDuration`: <ol><li> Uppspelningen avbryts `licenseDuration` sekunder efter uppspelningens början. </li><li> Om du vill tillåta att uppspelningen stoppas/återupptas under obegränsad tid utelämnar du `licenseDuration` (det kommer att vara oändligt som standard). I annat fall anger du hur lång tid slutanvändarna ska kunna utnyttja strömmen. </li></ol>

**Tabell 15: Frågeparametrar för tokenbegränsning**

| Frågeparameter | Beskrivning | Obligatoriskt? |
|--- |--- |--- |
| `expirationTime` | Förfallotid för denna token. Det här värdet MÅSTE vara en sträng i [RFC 339](https://www.ietf.org/rfc/rfc3339.txt) datum-/tidsformat i zondesignern för Z (&quot;Zulu time&quot;) eller ett heltal föregånget av ett +-tecken. Ett exempel på ett RFC 3339-datum/tid är 2006-04-14T12:01:10Z. <br> Om värdet är en sträng i  [RFC 339](https://www.ietf.org/rfc/rfc3339.txt) datum/tid-format representerar det ett absolut förfallodatum/tid för token. Om värdet är ett heltal som föregås av tecknet + tolkas det som ett relativt antal sekunder, från utgivningen, att token är giltig. `+60` anger till exempel en minut. <br> Maximal token- och standardtokenlivstid (om inget anges) är 30 dagar. | Nej |

**Tabell 16: Parametrar för korrelationsfråga**

| **Frågeparameter** | **Beskrivning** | **Obligatoriskt?** |
|---|---|---|
| `cookie` | Godtycklig sträng på upp till 32 tecken som finns i token och som loggas av tokeninlösenservern. Kan användas för att korrelera loggposter på inlösenservern och poster på tjänsteleverantörens servrar. | Nej |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Tabell 17: HTTP-svar**

| **HTTP-statuskod** | **Beskrivning** | **Content-Type** | **Entitetstexten innehåller** |
|---|---|---|---|
| `200 OK` | Inget fel. | `text/uri-list` | URL för hämtning av licens + token |
| `400 Bad Request` | Ogiltiga argument | `text/html` eller  `application/json` | Felbeskrivning |
| `401 Unauthorized` | Autentisering misslyckades | `text/html` eller  `application/json` | Felbeskrivning |
| `404 Not found` | Felaktig URL | `text/html` eller  `application/json` | Felbeskrivning |
| `50x Server Error` | Serverfel | `text/html` eller  `application/json` | Felbeskrivning |

**Tabell 18: Felkoder för händelse**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> Code </th> 
   <th class="entry"> Beskrivning </th> 
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
   <td> Ogiltig autentiseringstoken: &lt;information&gt; <p>Obs!  Detta kan inträffa om autentiseraren är fel eller när testnings-API:t används på *.test.expressplay.com med produktionsautentiseraren och vice versa. </p> <p importance="high">Obs!  Test SDK och Advanced Test Tool (ATT) fungerar endast med <span class="filepath"> *.test.expressplay.com </span>, medan produktionsenheter måste använda <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Otillräckliga tokens är tillgängliga </td> 
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
   <td> <span class="filepath"> barn </span> saknas </td> 
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
   <td> <span class="codeph"> child  </span> must be 64 characters long after the '^' </td> 
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
   <td> -6005 </td> 
   <td> Ogiltiga nyckeldata har angetts </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Ogiltig uthyrningstid har angetts </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Bindning av enhets-ID stöds inte för Widewin </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Värde för säkerhetsnivå saknas </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Ogiltigt säkerhetsnivåvärde </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Kontrollvärde för HDCP-utdata saknas </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Ogiltig licenslängd har angetts </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Det gick inte att generera Widewin-licensen </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Ogiltiga <span class="codeph"> WVExtension </span>-parametrar har angetts </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Alternativet Widewin har inaktiverats </td> 
  </tr> 
 </tbody> 
</table>