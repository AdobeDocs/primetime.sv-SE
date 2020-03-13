---
seo-title: Referens för serveregenskaper
title: Referens för serveregenskaper
uuid: 24a187fe-9b7d-411f-a358-d10c70a5dd0e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Referens för serveregenskaper{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Individualiseringsserver

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> Konfiguration </th> 
   <th class="entry"> Beskrivning </th> 
   <th class="entry"> Exempel </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Transportautentiseringsuppgifter </td> 
   <td>Transportautentiseringsuppgifterna används för att dekryptera begäranden som tas emot från klienten och signera svar som skickas tillbaka. Konfigurera <span class="filepath"> filen AdobeInitial.properties</span> korrekt med både sökvägen till transportautentiseringsfilen och det krypterade PKCS12-lösenordet. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [PKCS12 file containing the Individualization Transport cert and key] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Krypterat lösenord för PKCS12-fil] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Autentiseringsuppgifter för Individuell certifikatutfärdare </td> 
   <td>Individualiseringsservern använder autentiseringsuppgifterna för Individualization CA för att signera datorcertifikaten som den utfärdar. Konfigurera <span class="filepath"> filen AdobeInitial.properties</span> på rätt sätt med både sökvägen till I15N CA-inloggningsfilen och det krypterade PKCS12-lösenordet. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [PKCS12 file containing the Individualization CA cert and key] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Krypterat lösenord för PKCS12-fil] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Autentiseringsuppgifter för Individuell kryptering </td> 
   <td> Individualiseringsservern använder krypteringsinformationen för att kryptera känsliga filer som behöver överföras till Individualization-servrarna. Det här certifikatet stöder till exempel licensmigrering och används även för att kryptera privata DRM-nycklar för Individualization-servrarna. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Innehållscache </td> 
   <td>Dessa inställningar styr den plats från vilken personaliseringsservern hämtar innehåll och var innehållet cachas på disken. Personaliseringsservern kontrollerar om det finns nytt innehåll på innehållsservern när den startas och därefter med den frekvens/tid som anges av dessa egenskaper. <p>För On Premises Individualization Server har vi tagit med en inledande uppsättning innehållscachedata. Glöm inte att kopiera <i>innehållet</i> i cachemappen (inte själva cachemappen) till den konfigurerade platsen <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> . </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [katalog där lokalt innehåll ska lagras (normalt tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Webbserver att kontakta för ECI-information (<i>stöds inte i den här versionen</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Connection timeout, i sekunder] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Hur ofta du ska avfråga servern, i dagar (minimum är 1 dag)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Tid på dygnet för att avfråga servern, i minuter sedan midnatt] </li> 
    </ul> <p>Läs avsnittet <i>CRL- och ECI-filer</i> om hur du håller cacheminnet uppdaterat. </p> </td> 
  </tr> 
  <tr> 
   <td> Certifikatutfärdarens CRL </td> 
   <td> <p>Distributionsplatsen för listan över återkallade certifikat (CRL) ingår i varje datorcertifikat som utfärdas av Individualization-servern. Under verifieringen av datorcertifikatet på licensservern hämtas CRL från den distributionsplats som anges i certifikatet (eller läses från cachen om den redan har hämtats) och kontrolleras för att säkerställa att certifikatet inte har återkallats. Vi rekommenderar att du utför den här ändringen av serverkonfigurationen efter att du har gått igenom processen att skapa och distribuera certifikatutfärdarens lista över enskilda användare. Starta om Individualization-servern efter en konfigurationsändring. </p> <p>Om du vill ange URL:en för CRL-distributionsplatsen måste du ange <span class="filepath"> fältet AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> . </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL-distributionsplats] </li> 
    </ul> <p>Exempel: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>Licensservern bör automatiskt hämta denna lista när en licensförfrågan har hanterats. </p> <p importance="high">Obs! Distributionspunkten kontrolleras <i>inte</i> av Primetime DRM för giltighet. Du måste verifiera att URL:en är giltig. Fel som uppstår från en ogiltig URL visas inte förrän valideringsfel visas från licensservern. </p> </td> 
  </tr> 
  <tr> 
   <td> Loggning </td> 
   <td>Konfigurera vid behov <span class="filepath"> AdobeInitial.properties</span> för loggning. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Katalog där loggfiler skapas] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [Den lägsta nivån av loggmeddelanden som kan visas i loggarna <span class="codeph"> [DEBUG]| INFO]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefix för loggfiler. Datum/tid och filnamnstillägget ".log" läggs till i filnamnet] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Anger hur ofta loggarna rullas.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Rulla loggarna när de når den här storleken (loggarna rullar när antingen <span class="codeph"> RollInterval</span> eller <span class="codeph"> RollSize</span> nås, beroende på vilket som inträffar först)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true]| false ] Anger om en separat fil ska genereras som innehåller data som används av Adobe för att generera Individualization-rapporter.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefix för rapportloggfiler. Datum/tid och <span class="filepath"> .log</span> -tillägget läggs till i filnamnet. Egenskapen log<span class="codeph"> .Level</span> gäller inte för den här loggfilen, men <span class="codeph"> log.RollInterval</span> och <span class="codeph"> log.RollSize</span> gör det.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Övriga </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceInfo.key =</span> [Encrypted Base64 encoded key used to HMAC device info before include it in the machine token. Nyckeln kan vara annorlunda för Dev/Staging/Production-miljöerna, men måste vara densamma för alla servrar i en viss miljö. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Location of Key Gen Server (a single host/port, representing a pool of key servers) ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Hämta en annan uppsättning nycklar från KGS när så här många nycklar finns kvar i kön] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [Statussidan pingar KGS för att avgöra om den kan nå servern. Tidsgränsen uppnås om inget svar tas emot igen inom den angivna tiden.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Nyckelgenereringsserver {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> Konfiguration </th> 
   <th class="entry"> Beskrivning </th> 
   <th class="entry"> Exempel </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Nyckelgenerering </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Antal trådar som ska användas för att generera nycklar (ska vara lika med antalet processorer som finns på datorn)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Antal nycklar att generera per batch] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Katalog där nyckelbatchfiler ska lagras] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Maximalt antal nyckelbatchfiler att generera] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Loggning </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Katalog där loggfiler skapas] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefix för loggfiler. Datum/tid och <span class="filepath"> .log</span> -tillägget läggs till i filnamnet] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [Den lägsta nivån av loggmeddelanden som kan visas i loggarna] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Anger hur ofta loggarna rullas.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Rulla loggarna när de når den här storleken (loggarna rullar när antingen <span class="codeph"> RollInterval</span> eller <span class="codeph"> RollSize</span> nås, beroende på vilket som inträffar först)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
