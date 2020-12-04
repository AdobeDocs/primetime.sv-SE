---
seo-title: Översikt
title: Översikt
uuid: 19d05867-c210-4cd0-bc2f-5dd75f5774e5
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Listhanteraren för DRM-principuppdatering {#policy-update-list-manager}

Använd kommandoradsverktyget [!DNL AdobePolicyUpdateListManager.jar] (Primetime DRM Policy Update List Manager) för att skapa och hantera listor för DRM-principuppdatering och för att kontrollera om profiler har uppdaterats eller återkallats.

Innan du kör kommandoradsverktyget för listhanteraren för principuppdatering måste du ange egenskaper i *listhanteraren för principuppdatering och egenskaperna för listhanteraren för återkallning* i konfigurationsfilen.

>[!NOTE]
>
>Du kan också ange alla egenskaper för listhanteraren för principuppdatering från kommandoraden.

## Kommandoradsanvändning {#policy-update-list-manager-command-line-usage} för listhanteraren för principuppdatering

**Skapa en principuppdateringslista:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` anger namnet på filen som DRM-principuppdateringslistan skrivs till.

**Visa en befintlig principuppdateringslista:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` Namnet på listfilen för principuppdatering.

**Tabell 4: Kommandoradsalternativ**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namn och plats för konfigurationsfilen. </p> <p class="- topic/p ">Om du inte anger ett namn eller en plats söker DRM Policy Update List Manager efter <span class="filepath"> flashaccesstools.properties </span> i den aktuella arbetskatalogen. </p> <p>Obs!  De alternativ som du anger på kommandoraden åsidosätter de alternativ som du anger i konfigurationsfilen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d filnamn  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om DRM-principens uppdateringslista. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e datum  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Valfritt) Utgångsdatumet för DRM-principuppdateringslistan. </p> <p>Använd formatet <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span> (t.ex. 2009-01-31-14:30:00 representerar 31 januari klockan 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filnamn [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lägger till alla poster från den befintliga DRM-principuppdateringslistan. Du kan bara ange en befintlig fil. </p> <p class="- topic/p ">Om den befintliga listan har signerats med en annan autentiseringsuppgift än den som används för att signera den nya listan, måste du ange dess certifikatfil för att verifiera dess signatur. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o </span> inte har angetts inträffar ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om målfilen redan finns skriver du över den utan att fråga. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Valfritt) Återkallar DRM-principens ID på det angivna datumet. Du kan ange en valfri orsakskod, orsakstext och orsak-URL. Du måste ange en tom sträng "" för att ange att inget värde har angetts för de valfria parametrarna. Du kan ange datumet i <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span> i dessa format. Exempel: 2008-12-1 eller 2008-12-1-00:00:00 representerar midnatt den 1 december 2008). Om du inte anger något datum används det aktuella datumet automatiskt. Därför måste orsakskoden vara större än eller lika med 0. Du kan också ange flera -r-alternativ. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utför samma åtgärd som alternativet <span class="codeph"> -r </span>. DRM-principens identifierare extraheras dock från en angiven fil. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilnamn " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Ersätter alla matchande DRM-principer i en licensbegäran med den här DRM-principen med den angivna orsakskoden (valfritt), orsakstexten (valfritt) och orsak-URL:en (valfritt). </p> <p>En tom sträng "" anger att du inte har angett något värde för de valfria parametrarna. </p> <p>Orsakskoden måste vara större än eller lika med <span class="codeph"> 0 </span>. Du kan ange flera alternativ för <span class="codeph"> -u </span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Konfigurationsegenskaper {#configuration-properties}

Följande egenskaper för Primetime DRM Policy Update List Manager anger en PKCS12-fil som innehåller autentiseringsuppgifter för undertecknande av spärrlistor (licensservercertifikat) tillsammans med ett lösenord.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`