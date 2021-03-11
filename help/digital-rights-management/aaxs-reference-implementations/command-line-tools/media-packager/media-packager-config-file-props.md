---
title: Egenskaper för konfigurationsfil
description: Egenskaper för konfigurationsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Egenskaper för konfigurationsfil {#configuration-file-properties}

Innan du kör Media Packager anger du värden för egenskaperna för Media Packager. Konfigurationsfilen anger följande egenskaper. För egenskapsnamn som innehåller* n* representerar *n* ett heltal som börjar med 1 och ökar för varje instans av egenskapen.

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
   <td colname="2" class="- topic/entry ">Anger om skriptdata ska krypteras i FLV-filer. <i class="+ topic/ph hi-d/i "></i> onMetaData- och  <i class="+ topic/ph hi-d/i "></i> onXMPscript-datataggar krypteras aldrig, även om det här alternativet är aktiverat. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger videokrypteringsnivån. Värdet high används för att kryptera allt videoinnehåll, medan värdena medium och low används för att kryptera delar av videoinnehållet för F4V-filer som innehåller H.264-innehåll. </p> <p class="- topic/p ">värde = <span class="codeph"> högt | medium | låg</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om värdet är större än 0 krypteras inte det angivna antalet sekunder med innehåll i början av filen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certifikatfilen för licensservern som används för att kryptera nyckeln. Egenskapen <span class="codeph"> encrypt.keys.asymmetric.certfile</span> anger en fil som endast innehåller certifikatet (antingen PEM- eller DER-format tillåts). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Den här egenskapen används upprepade gånger för att skapa en lista med profiler som ska tillämpas på innehållet. <span class="codeph"> är </span> ett heltal vars värde är 1 eller högre. Klienten använder den första instansen som standard. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Licensserverns URL. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Transportcertifikatet för licensservern. This property specifies a <span class="filepath"> .cer</span> file that contains the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12-filen som innehåller autentiseringsuppgifter för paketering för signering av innehåll. <span class="codeph"> encrypt.sign.certfile</span> ska referera till en <span class="filepath"> .pfx</span>-fil som innehåller ett certifikat och en privat nyckel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lösenordet som används för att skydda filen som anges av <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger den lägsta serverversion som krävs för att utfärda licenser för innehållet som paketeras. Ange x (Adobe Access x.0) där x = större versionsnummer. Servrar före Adobe Access 3.0 stöder inte den här inställningen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.flyttcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om en princip <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> kräver domänregistrering med en server som använder ett annat transportcertifikat än vad som anges i <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span> måste domänens transportcertifikat anges. </p> <p class="- topic/p ">This property specifies a file that contains the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Ange licensnyckel. Om ingen nyckel anges genereras nyckeln slumpmässigt. När nyckelrotation inte är aktiverad är det den här nyckeln som används för att kryptera innehållet. </p> <p class="- topic/p ">När tangentrotation är aktiverad används den här tangenten för att skydda rotationstangenterna. Nyckeln måste vara 16 byte lång och anges som hex-värden. Det är valfritt att använda blanksteg mellan hexadecimala värden. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger om tangentrotation är aktiverad. Om värdet är false (standard) inaktiveras nyckelrotation och det överordnad CEK-värdet används för att kryptera alla samplingar i innehållet. </p> <p class="- topic/p ">Om värdet är true aktiveras nyckelrotation och olika nycklar kan användas för att kryptera delar av innehållet. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sekvens med roterade nycklar som används för att kryptera innehåll när nyckelrotation är aktiverad. Om inga nycklar anges genereras nycklarna slumpmässigt. Nycklarna måste vara 16 byte långa och anges som Hex-värden. </p> <p class="- topic/p ">Det är valfritt att använda blanksteg mellan hexadecimala värden. <i class="+ topic/ph hi-d/i ">Från och med 1 </i> måste antalet öka monotont. När flera nycklar anges kommer nycklarna att bläddras igenom i den ordning som anges. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger det intervall (i sekunder) under vilket en rotationsnyckel ska användas för att kryptera innehållssamplingar. </p> <p class="- topic/p ">När den här tiden i innehållet har krypterats används nästa rotationsnyckel. Om tangentrotation är aktiverad och inget intervall anges, roteras tangenterna var 15:e minut. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om true finns det ingen licensserver som licenserna kan hämtas från. Licenser måste vara inbäddade eller köpta separat. Standardvärdet är false om det inte anges. Stöds endast i Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>

