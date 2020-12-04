---
seo-title: Översikt
title: Översikt
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# DRM-licensgenerator {#license-generator}

Använd [!DNL AdobeLicenseGenerator.jar] för att generera licenser utan att klienten behöver skicka en licensbegäran till en server. Du kan sedan bädda in en förgenererad licens i innehållet eller leverera licensen till klienten via andra mekanismer, till exempel en enkel HTTP-webbserver.

## Licensgeneratorns kommandoradsanvändning {#license-generator-command-line-usage}

**Generera en licens:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` - Innehåller Adobe Primetime DRM-metadata.

   Du kan hämta den här filen från skyddat innehåll med `-d -m`-alternativen i Media Packager.

**Visa en tidigare genererad licens:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` - Innehåller en Adobe Primetime DRM-licens som genererats av licensgeneratorn.

**Tabell 6: Alternativ**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namn och plats för konfigurationsfilen. </p> <p class="- topic/p ">Om du inte anger ett namn eller en plats söker DRM-licensgeneratorn efter <span class="filepath"> flashaccesstools.properties</span> i den aktuella arbetskatalogen. </p> <p>Obs!  De alternativ som du anger på kommandoraden åsidosätter de alternativ som du anger i konfigurationsfilen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensfil</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Visar information om en licens som redan har skapats. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Skapar en lövlicens och sparar utdata i en angiven fil. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filnamn</span> </td> 
   <td colname="2" class="- topic/entry "> Anger de innehållets metadata som du behöver för att generera en licens. Det här alternativet krävs för att generera en licens. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o</span> inte har angetts inträffar ett fel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns kan du skriva över den utan att tillfrågas. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Om metadata innehåller flera DRM-principer kan du ange hur många DRM-profiler du kan använda för att generera en licens. </p> <p>Om du inte anger antalet DRM-principer tillämpas den första DRM-principen automatiskt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r mottagare-cert</span> </td> 
   <td colname="2" class="- topic/entry ">Skapar en licens för en angiven mottagare. Du kan använda ett enhets- eller domäncertifikat och du kan ange flera <span class="+ topic/ph pr-d/codeph codeph"> -r </span>alternativ för att skapa en licens för flera mottagare. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Skapar en rotlicens och sparar utdata i en fil som du anger. </td> 
  </tr> 
 </tbody> 
</table>

## Egenskaper för konfigurationsfil {#configuration-file-properties}

Innan du kör licensgeneratorn måste du ange värden för licensgeneratoregenskaperna i konfigurationsfilen.

>[!NOTE]
>
>För egenskapsnamn som innehåller *n* representerar *n* ett heltal som börjar med 1 och ökar för varje instans av egenskapen.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Egenskap </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Anger den lägsta klientversion som stöds för tillfället. Om du inte anger den här egenskapen stöds alla versioner automatiskt som standard. </p> <p>Du kan ange det här värdet för att styra hur äldre klienter ska uppfylla de licenskrav som de inte stöder. Ange <span class="codeph"> x</span> (för Adobe Primetime DRM x.0) där <span class="codeph"> x</span> representerar ett större versionsnummer. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server-certifikat, som är ett Adobe-utfärdat licensservercertifikat som används av Key Server. Det här certifikatet används endast om metadata-/DRM-principen anger att en nyckelserver krävs för nyckelleverans till iOS-enheter. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> PKCS12-filen som innehåller autentiseringsuppgifterna för licensservern för undertecknande av licenser. Den här egenskapen måste referera till en pfx-fil som innehåller ett certifikat och en privat nyckel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">Lösenordet som skyddar filen som du har angett med alternativet <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span>. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Om du genererar domänbundna licenser måste du ange ett eller flera certifikat för domän-certifikatutfärdare för att ange vilka domänmyndigheter som licensutfärdaren kan lita på. </p> <p>Om licensmottagaren är ett domäncertifikat som inte har utfärdats av någon av de angivna domänkontrollanterna går det inte att generera någon licens. This property specifies a <span class="filepath"> .cer</span> file that includes the certificate in the PEM or the DER format. <span class="codeph"></span> måste öka monotont, med början från 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12-fil (tillval) som innehåller ytterligare autentiseringsuppgifter för licensservern för dekryptering av CEK i metadata och DRM-principen. Du kan konfigurera ytterligare autentiseringsuppgifter om innehåll tidigare har paketerats med ett annat licensservercertifikat än de autentiseringsuppgifter som har angetts med <span class="codeph"> licensgen.sign.certfile</span>. Den här egenskapen måste referera till en <span class="filepath"> .pfx</span>-fil som innehåller ett certifikat och en privat nyckel. <span class="codeph"></span> måste öka monotont, med början från 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>Lösenordet används för att skydda filen som du har angett med egenskapen<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span>. </p> </td> 
  </tr> 
 </tbody> 
</table>