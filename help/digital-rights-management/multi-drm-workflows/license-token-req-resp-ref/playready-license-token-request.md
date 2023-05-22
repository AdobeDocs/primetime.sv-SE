---
description: Licenstoken för PlayReady ger tillgång till produktions- och testtjänster.
title: PlayReady-licenstokenbegäran/svar
exl-id: 12f925f7-336b-42b2-95a9-e806801bab8c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# PlayReady-licenstokenbegäran/svar {#playready-license-token-request-response}

Licenstoken för PlayReady ger tillgång till produktions- och testtjänster.

Denna HTTP-begäran returnerar en token som kan läsas in för en PlayReady-licens.

**Metod: GET, POST** (med en www-url-encoded body som innehåller parametrar för båda metoderna)

**URL:er:**

* **Produktion:** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Test:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Exempelbegäran:**

   ```
   <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
   https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
    <ExpressPlay customer authenticator identifier>
    &kid=<CEKSID>
    &contentKey=<CEK>
    &rightsType=BuyToOwn
    &analogVideoOPL=0
    &compressedDigitalAudioOPL=0
    &compressedDigitalVideoOPL=0
    &uncompressedDigitalAudioOPL=0
    &uncompressedDigitalVideoOPL=0
   </xref href="https:>
   ```

* **Exempelsvar:**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## Frågeparametrar för begäran {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Tabell 9: Parametrar för tokenfråga**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Frågeparameter</b> </th> 
   <th class="entry"><b>Beskrivning</b> </th> 
   <th class="entry"><b>Obligatoriskt?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>Det här är er API-nyckel för era kunder, en för era produktions- och testmiljöer. Det finns på fliken Admin Dashboard för ExpressPlay. </p> </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>Antingen <span class="codeph"> html</span> eller <span class="codeph"> json</span>. If <span class="codeph"> html</span> (standardvärdet) en HTML-representation av eventuella fel anges i svarets entitetstext. <p>If <span class="codeph"> json</span> anges returneras ett strukturerat svar i JSON-format. Se <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON-fel</a> för mer information. </p> <p>MIME-typen för svaret är antingen <span class="codeph"> text/uri-list</span> om framgång, <span class="codeph"> text/html</span> för felformatet HTML, eller <span class="codeph"> application/json</span> för JSON-felformat. </p> </td> 
   <td> Nej </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 10: Parametrar för licensfråga**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Frågeparameter</b> </th> 
   <th class="entry"><b>Beskrivning</b> </th> 
   <th class="entry"><b>Obligatoriskt?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>En hexadecimal sträng på 4 byte som representerar licensflaggorna. Den måste anges till"00000001" för en permanent licens. <p>Obs! Hyreslicenser (<span class="codeph"> rightsType=Hyr</span>) MÅSTE vara beständig. </p> </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Nyckelkrypteringsnyckel (KEK). Tangenter lagras krypterade med en KEK med hjälp av en nyckelomslutningsalgoritm (AES Key Wrap, RFC3394). </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> grabb</span> </td> 
   <td>En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln eller en sträng <span class="codeph"> ^someString'</span>. Längden på strängen följt av '^' får inte vara längre än 64 tecken. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> En hexadecimal strängrepresentation av den krypterade innehållsnyckeln. </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> En 16 byte hexadecimal strängbeteckning för innehållskrypteringsnyckeln </td> 
   <td>Ja, om inte <span class="codeph"> kek</span> och <span class="codeph"> ek</span> eller <span class="codeph"> grabb</span> tillhandahålls </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Anger typen av rättigheter. Måste vara <span class="codeph"> KöpTillÄger</span> eller <span class="codeph"> Uthyrning</span>. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> hyrtidSluttid</span> </td> 
   <td>Uthyrningens slutdatum. Detta värde MÅSTE vara i formatet"RFC 3339" _ datum/tid i formatet"Z" zonbeteckning ("Zulu time") eller ett heltal föregånget av tecknet"+". <p>Om värdet är ett <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> datum-/tidsformat, representerar då ett absolut förfallodatum/tid för licensen. Ett exempel på ett RFC 3339-datum/tid är 2006-04-14T12:01:10Z. </p> <p> Om värdet är ett heltal som föregås av ett plustecken (+) tas det som ett relativt antal sekunder från den tidpunkt då variabeln utfärdas. Innehållet kan inte spelas upp efter den här tiden. Endast giltigt om <span class="codeph"> rightsType</span> är <span class="codeph"> Uthyrning</span>. </p> </td> 
   <td>Ja, när <span class="codeph"> rightsType</span> är <span class="codeph"> Uthyrning</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> hyrtid.playDuration</span> </td> 
   <td>Tid i sekunder som innehållet kan spelas upp när uppspelningen har startat. Endast giltigt om <span class="codeph"> rightsType</span> är Uthyrning. </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> Heltalsvärde som anger utdataskyddsnivån för analog video. Giltigt intervall: 0-999. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> Heltalsvärde som anger utdataskyddsnivån för komprimerat digitalt ljud. Giltigt intervall: 0-999. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> Heltalsvärde som anger utdataskyddsnivån för komprimerad digital video. Giltigt intervall: 0-999. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Heltalsvärde som anger utdataskyddsnivån för okomprimerat digitalt ljud. Giltigt intervall: 0-999. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> Heltalsvärde som anger utdataskyddsnivån för okomprimerad digital video. Giltigt intervall: 0-999. </td> 
   <td> Ja </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Nödvändigt beteende när utdata är okända. Tillåtna värden: <span class="codeph"> Tillåt</span>, <span class="codeph"> Tillåt inte</span> eller <span class="codeph"> SDOnly</span> </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> Ett hexadecimalt värde på 4 byte som anger flaggorna för andra alternativ för utdatakontroll </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>Ett ord med fyra bokstäver som representerar en 32-bitars identifierare för ett tillägg. Varje teckens 8-bitars ASCII-kod är motsvarande 8-bitars byte-del av identifieraren. Identifierarvärdet 0x61626364 (hexadecimalt) skrivs till exempel med "<span class="codeph"> abcd</span>', eftersom ASCII-koden för"a" är 0x61 osv. </td> 
   <td> Nej </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> En base64-kodad sträng i tillägget. </td> 
   <td>Ja, när <span class="codeph"> extensionType</span> har angetts. </td> 
  </tr> 
 </tbody> 
</table>

## Svar {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Tabell 11: HTTP-svar**

| **HTTP-statuskod** | **Beskrivning** | **Content-Type** | **Entitetstexten innehåller** |
|---|---|---|---|
| `200 OK` | Inget fel. | `text/uri-list` | URL och token för licenshämtning |
| `400 Bad Request` | Ogiltiga argument | `text/html` eller `application/json` | Felbeskrivning |
| `401 Unauthorized` | Autentisering misslyckades | `text/html` eller `application/json` | Felbeskrivning |
| `404 Not found` | Felaktig URL | `text/html` eller `application/json` | Felbeskrivning |
| `50x Server Error` | Serverfel | `text/html` eller `application/json` | Felbeskrivning |

**Tabell 12: Felkoder för händelse**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Code</b> </th> 
   <th class="entry"><b>Beskrivning</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Ogiltig förfallotid för token: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Ogiltig IP-adress </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Ogiltig krypteringsnyckel för innehåll: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Ogiltiga utdatakontrollflaggor har angetts: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Autentiseringstoken måste anges </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td>Ogiltig autentiseringstoken: &lt;details&gt; <p>Obs! Detta kan inträffa om autentiseraren är fel eller när testnings-API:t används på *.test.expressplay.com med produktionsautentiseraren och vice versa. </p> <p importance="high">Obs! Test SDK och Advanced Test Tool (ATT) fungerar endast med <span class="filepath"> *.test.expressplay.com</span>, medan produktionsenheter måste använda <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td> ExpressPlay Admin-fel: &lt;details&gt; </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> måste vara koda 4 byte </td> 
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
   <td> -4018 </td> 
   <td>Saknas <span class="codeph"> grabb</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Det gick inte att hämta innehållsnyckeln från nyckellagringstjänsten </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> grabb</span> måste vara 32 hexadecimala tecken långa </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> grabb</span> måste innehålla 64 tecken efter ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>Ogiltig <span class="codeph"> grabb</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Ogiltig krypterad <span class="codeph"> key</span> eller kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Okänt utdatatypsfel </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> Alternativet PlayReady är inaktiverat för den här tjänsten </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Ogiltiga allmänna flaggor </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> Enhets-ID måste vara 32 hexadecimala tecken långt </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> Ogiltigt enhets-ID </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> OPL-värde saknas </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>Endast en av <span class="codeph"> kek</span> eller <span class="codeph"> contentKey</span> kan anges </td> 
  </tr> 
 </tbody> 
</table>
