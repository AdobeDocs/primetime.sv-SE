---
description: 'null'
seo-description: 'null'
seo-title: Översikt
title: Översikt
uuid: f4474837-9460-479d-89c2-dd697e0fb997
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 0%

---


# DRM Media Packager {#media-packager}

Använd Media Packager ( [!DNL AdobePackager.jar]) för att ange en DRM-princip som ska gälla för ditt innehåll och för att ange vilken del av innehållet som ska krypteras. Du kan till exempel ange att paketeraren ska kryptera videodata, men inte ljuddata.

Innan du kör [!DNL AdobePackager.jar]måste du ange egenskaper i avsnittet Egenskaper för Media Packager i konfigurationsfilen.

>[!NOTE]
>
>Du kan också ange alla egenskaper för Media Packager från kommandoraden.

## Kommandoradsanvändning för Media Packager {#media-packager-command-line-usage}

**Paketera en fil:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` - Namnet på filen som du vill kryptera.
* `dest` - Namnet på den resulterande krypterade filen.

   Om du anger en katalog sparas den krypterade filen automatiskt i den angivna katalogen med samma filnamn som du angav som källfil. Du kan dock inte ange en målkatalog som innehåller källfilen.

**Paketera flera filer med samma nyckel** (för stöd för flera bitar):

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` - En serie mellanrumsavgränsade källposter för de filer som du vill kryptera.
* `dest-directory` - Målkatalogen där du vill skriva krypterat innehåll. De krypterade filerna sparas automatiskt i den här katalogen med samma filnamn som källfilerna. Målkatalogen kan dock inte innehålla några källfiler.

**Visa information om en krypterad fil:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**Visa information om en metadatafil:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` är en [!DNL .metadata] fil som innehåller DRM-metadata.

>[!NOTE]
>
>Under paketeringen kan Media Packager inte längre generera en [!DNL .header] fil som standard. Om du vill generera en [!DNL .header] fil använder du `-h` alternativet under paketeringen.

**Tabell 3: Alternativ**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namn och plats för konfigurationsfilen. </p> <p class="- topic/p ">Om du inte anger ett namn eller en plats söker DRM Media Packager efter <span class="filepath"> flashaccesstools.properties </span> i den aktuella arbetskatalogen. </p> <p>Obs!  De alternativ som du anger på kommandoraden åsidosätter de alternativ som du anger i konfigurationsfilen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedFile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gör att du kan visa information om en fil som redan har paketerats. </p> <p class="- topic/p ">Käll- och målfilerna är inte obligatoriska. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafil </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Här kan du visa information om befintliga metadata. </p> <p class="- topic/p ">Käll- och målfilerna är inte obligatoriska. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extraherar DRM-principer från en paketerad fil när du använder det här alternativet tillsammans med <span class="codeph"> -d- </span> alternativet. </p> <p class="- topic/p ">En fil skapas automatiskt i samma katalog där den krypterade filen finns med ett filnamn och en DRM-principidentifierare. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extraherar DRM-huvudet från en paketerad fil när du använder det här alternativet tillsammans med <span class="codeph"> -d- </span> alternativet. </p> <p class="- topic/p ">En fil skapas automatiskt i samma katalog där den krypterade filen finns med filnamnet och filnamnstillägget <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger en unik identifierare för det här innehållssegmentet. </p> <p class="- topic/p ">Om du inte anger någon identifierare används målfilens namn automatiskt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> värde </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger en anpassad nyckel/värde som ska läggas till i innehållets metadata. </p> <p class="- topic/p ">Du kan ange flera <span class="codeph"> -k- </span> alternativ. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrahera metadata från en paketerad fil när du använder det här alternativet tillsammans med <span class="codeph"> -d- </span> alternativet. </p> <p class="- topic/p ">En fil skapas automatiskt i samma katalog som den krypterade filen med ett filnamn och ett <span class="codeph"> .metadata- </span> tillägg. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. </p> <p class="- topic/p ">Om målfilen redan finns och <span class="codeph"> -o inte </span> är inställd inträffar ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Skriver över målfilen utan att du tillfrågas om den inte redan finns. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> filnamn [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namnet på filen som innehåller DRM-principen. </p> <p class="- topic/p ">Om DRM-principen kräver domänregistrering hos en server som använder ett annat transportcertifikat än det som du har angett i egenskapsfilen, måste du ange domänens transportcertifikat. </p> <p class="- topic/p ">Du kan ange flera <span class="codeph"> -p- </span> alternativ. Klienten använder alltid det första alternativet som standard. De värden som du har angett på kommandoraden har högre prioritet än de som du har angett i konfigurationsfilen. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Konfigurationsegenskaper {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>För egenskapsnamn som innehåller* n* representerar *n* ett heltal som börjar med 1 och ökar för varje instans av egenskapen.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Egenskap </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> Anger om videoinnehåll ska krypteras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Anger om ljud ska krypteras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Anger om skriptdata ska krypteras i mp4s. </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> - och <i class="+ topic/ph hi-d/i ">onXMP</i> -skriptdatataggar krypteras aldrig, även om du aktiverar det här alternativet. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger videokrypteringsnivån. </p> <p class="- topic/p ">Värdet <span class="codeph"> high</span> används för att kryptera allt videoinnehåll, medan värden för <span class="codeph"> medium</span> och <span class="codeph"> low</span> används för att kryptera delar av videoinnehållet för mp4-filer som innehåller H.264-innehåll. </p> <p class="- topic/p ">value = <span class="codeph"> high | medium | låg</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om värdet är större än 0 krypteras inte det angivna antalet sekunder av innehållet i början av filen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certifikatfilen för licensservern som används för att kryptera nyckeln. </p> <p class="- topic/p ">Egenskapen <span class="codeph"> encrypt.keys.asymmetric.certfile</span> anger en fil som endast innehåller certifikatet (antingen PEM- eller DER-format tillåts). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den här egenskapen används upprepade gånger för att skapa en lista med DRM-principer som ska tillämpas på innehållet. <span class="codeph"> n</span> representerar ett heltal vars värde är 1 eller högre. Klienten använder den första instansen som standard. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensserverns URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Transportcertifikatet för licensservern. </p> <p class="- topic/p ">This property specifies a <span class="filepath"> .cer</span> file that includes the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12-filen som innehåller autentiseringsuppgifter för paketering för signering av innehåll. </p> <p class="- topic/p ">Filen <span class="codeph"> encrypt.sign.certfile</span> måste referera till en <span class="filepath"> .pfx</span> -fil som innehåller ett certifikat och en privat nyckel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lösenordet som du kan använda för att skydda filen som har angetts av <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger den lägsta serverversion som krävs för att utfärda licenser för innehållet som paketeras. </p> <p class="- topic/p ">Ange x (för Primetime DRM x.0) där x representerar ett större versionsnummer. Eventuella versioner av servrar före Adobe Primetime version 3.0 stöder inte den här inställningen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.flyttcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om en DRM-princip <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> kräver domänregistrering med en server som stöder ett annat transportcertifikat än det som du har angett i <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, måste du ange domänens transportcertifikat. </p> <p class="- topic/p ">This property specifies a file that includes the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger en licensnyckel. </p> <p class="- topic/p ">Om du inte anger någon tangent genereras nyckeln slumpmässigt. Om du inte aktiverar tangentrotation kan du använda den här nyckeln för att kryptera innehåll. </p> <p class="- topic/p ">När du aktiverar tangentrotation kan du använda den här tangenten för att skydda rotationstangenterna. Nyckeln måste vara 16 byte lång och anges som hex-värden. Det är valfritt att använda mellanrum mellan hexadecimala värden. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger om tangentrotation är aktiverad. </p> <p class="- topic/p ">Om värdet är false, vilket är standardinställningen, inaktiveras tangentrotation och den överordnad CEK används för att kryptera alla samplingar i innehållet. </p> <p class="- topic/p ">Om värdet är true aktiveras nyckelrotation och olika nycklar kan användas för att kryptera segment av vilket innehåll som helst. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sekvens med roterade nycklar som du kan ange för att kryptera innehåll när nyckelrotation är aktiverad. </p> <p class="- topic/p ">Om du inte anger några tangenter genereras nycklarna slumpmässigt. Nycklarna måste vara 16 byte långa och anges som Hex-värden. </p> <p class="- topic/p ">Det är valfritt att använda mellanrum mellan hexadecimala värden. <i class="+ topic/ph hi-d/i ">n</i> måste öka monotont, med början från 1. När du anger flera tangenter bläddras nycklarna igenom i den ordning som du har angett. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger tidsintervallet i sekunder under vilket du kan använda en rotationsnyckel för att kryptera innehållssamplingar. </p> <p class="- topic/p ">När tidsintervallet har gått ut då innehållet har krypterats, tillämpas nästa rotationsnyckel. Om du har aktiverat tangentrotation men inte har angett något tidsintervall, roteras tangenterna automatiskt var 15:e minut. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om det här alternativet är true är ingen licensserver som kan hämta licenser från tillgänglig. </p> <p class="- topic/p ">Licenser måste vara inbäddade eller köpta separat. Standardvärdet är false om du inte anger ett annat värde. Det här alternativet stöds bara i Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>