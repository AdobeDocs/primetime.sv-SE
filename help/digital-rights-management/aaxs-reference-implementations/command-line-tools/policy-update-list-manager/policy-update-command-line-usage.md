---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 1c3a450d-5d9c-4437-89dd-1bd8719268b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Kommandoradsanvändning {#command-line-usage}

Listhanteraren för principuppdatering finns i katalogen \Reference Implementation\Command Line Tools på dvd:n. Använd följande syntax för att skapa en principuppdateringslista:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` anger var listan över principuppdateringar ska skrivas.

Om du vill visa en befintlig principuppdateringslista använder du följande syntax:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

Följande tabell innehåller beskrivningar av kommandoradsalternativen som visas i syntaxen ovan:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger platsen för konfigurationsfilen. Om det här alternativet inte används söker principuppdateringslisthanteraren efter <span class="filepath"> flashaccesstools.properties </span> i arbetskatalogen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d filnamn  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om principuppdateringslistan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e datum  </span> </td> 
   <td colname="2" class="- topic/entry "> (Valfritt) Giltighetsdatumet för principuppdateringslistan. Använd formatet <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span> (t.ex. 2009-01-31-14:30:00 representerar 31 januari klockan 2:30 PM). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filnamn [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Lägger till alla poster från den befintliga principuppdateringslistan. Endast en befintlig fil kan anges. </p> <p class="- topic/p ">Om den befintliga listan signerades med en annan autentiseringsuppgift än den som används för att signera den nya listan anger du dess certifikatfil så att signaturen kan verifieras. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o </span> inte har angetts returneras ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om målfilen redan finns skriver du över den utan att fråga. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Valfritt) Återkallar princip-ID på det angivna datumet. En valfri orsakskod, orsakstext och orsak-URL kan också anges. Ange en tom sträng "" för att ange att det inte finns något värde för de valfria parametrarna. Ange datumet som <span class="+ topic/ph pr-d/codeph codeph"> åååå-mm-dd </span> eller <span class="+ topic/ph pr-d/codeph codeph"> ååå-mm-dd-h24:min:sek </span> (till exempel 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1, 2008). Om inget datum anges används aktuellt datum. Orsakskoden måste vara större än eller lika med 0. Flera -r-alternativ kan anges. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utför samma åtgärd som flaggan -r, men extraherar principidentifieraren från den angivna filen. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilnamn " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Ersätter alla matchande principer i en licensbegäran med den här principen med den angivna orsakskoden (valfritt), orsakstexten (valfritt) och orsak-URL:en (valfritt). </p> <p>Ange en tom sträng "" för att ange att det inte finns något värde för de valfria parametrarna. </p> <p>Orsakskoden måste vara större än eller lika med <span class="codeph"> 0 </span>. Flera <span class="codeph"> -u </span>-alternativ kan anges. </p> </td> 
  </tr> 
 </tbody> 
</table>

