---
title: DRM Revocation List Manager
description: DRM Revocation List Manager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# DRM Revocation List Manager {#policy-revocation-list-manager}

Använd kommandoradsverktyget Primetime DRM Revocation List Manager ( [!DNL AdobeRevocationListManager.jar]) för att skapa och hantera återkallningslistor och för att kontrollera om profiler har återkallats.

Innan du kör [!DNL AdobeRevocationListManager.jar] måste du ange egenskaper i *listhanteraren för principuppdatering och egenskaper för spärrlistehanteraren* i konfigurationsfilen.

>[!NOTE]
>
>Du kan också ange alla egenskaper för Hanteraren för spärrlista från kommandoraden.

## Kommandoradsanvändning {#revocation-list-manager-command-line-usage} för Hanteraren för återkallningslista

```
java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` Anger namnet på filen där egenskaperna för återkallningslistan sparas.
* `crlNumber` representerar ett versionsnummer som inte är negativt för listan över spärrade certifikat (CRL). Du måste öka det här antalet varje gång CRL-listan uppdateras.

**Tabell 5: Alternativ för kommandorad**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Kommandoradsalternativ </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Anger namn och plats för konfigurationsfilen. </p><p class="- topic/p ">Om du inte anger ett namn eller en plats söker DRM Revocation List Manager efter <span class="filepath"> flashaccesstools.properties</span> i den aktuella arbetskatalogen. </p><p>Obs!  De alternativ som du anger på kommandoraden åsidosätter de alternativ som du anger i konfigurationsfilen. </p>Anger platsen för konfigurationsfilen. Om du inte använder det här alternativet söker Revocation List Manager efter <span class="filepath"> flashaccesstools.properties</span> i arbetskatalogen. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d filnamn</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om återkallningslistan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e datum</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Valfritt) Giltighetsdatumet för listan över återkallade certifikat. Använd något av följande format: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sek</span> </li> 
     </ul>Exempel: 2009-01-31-14:30:00 representerar 31 januari klockan 2:30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filnamn[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Lägger till alla poster från den befintliga återkallningslistan. Du kan bara ange en befintlig fil. </p> <p class="- topic/p ">Om den befintliga listan har signerats med en annan autentiseringsuppgift än den du använde för att signera den nya listan, måste du ange certifikatfilen bredvid att verifiera signaturen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o</span> inte har angetts inträffar ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns kan du skriva över den utan att tillfrågas. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issurName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Återkallar certifikatet som har identifierats av <span class="codeph"> utfärdarnamn</span> och <span class="codeph"> serienummer</span> på det angivna datumet. <span class="codeph"> utfärdarnamn</span> måste använda 509-namnformatet. Till exempel <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>Du måste ange serienumren i ett hexadecimalt format. Du måste även ange återkallningsdatumet i något av följande format: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sek</span> </li> 
     </ul>Exempel: 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1 december 2008. Om du inte anger återkallelsedatumet används det aktuella datumet automatiskt. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Konfigurationsegenskaper {#configuration-properties}

Du måste använda autentiseringsuppgifter för att signera återkallningslistor. Följande egenskaper för spärrlistehanteraren anger en PKCS12-fil som innehåller autentiseringsuppgifter för undertecknande av spärrlistor (licensservercertifikat) tillsammans med lösenordet för certifikatet:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`