---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Kommandoradsanvändning {#command-line-usage}

Listhanteraren för återkallande finns i katalogen \Reference Implementation\Command Line Tools på dvd:n. Om du vill köra verktyget använder du någon av följande syntaxer:

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

* `destfile` anger var återkallningslistan ska skrivas.
* `crlNumber` är ett versionsnummer som inte är negativt för listan över spärrade certifikat (CRL). Numret ska ökas varje gång CRL uppdateras.

Följande tabell innehåller beskrivningar av kommandoradsalternativen som visas i syntaxen ovan:

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
   <td colname="2" class="- topic/entry ">Anger platsen för konfigurationsfilen. Om det här alternativet inte används söker återkallningslisthanteraren efter <span class="filepath"> flashaccesstools.properties</span> i arbetskatalogen. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d filnamn</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om återkallningslistan. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e datum</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Valfritt) Giltighetsdatumet för listan över återkallade certifikat. Använd formatet <span class="+ topic/ph pr-d/codeph codeph">åååå-mm-dd</span> eller <span class="+ topic/ph pr-d/codeph codeph">ååå-mm-dd-h24:min:sek</span> (t.ex. 2009-01-31-14:30:00 representerar 31 januari klockan 2:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filnamn[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Lägger till alla poster från den befintliga återkallningslistan. Endast en befintlig fil kan anges. <p class="- topic/p ">Om den befintliga listan signerades med en annan autentiseringsuppgift än den som används för att signera den nya listan anger du certifikatfilen härnäst så att signaturen kan verifieras. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och -o inte är inställd returneras ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns skriver du över den utan att fråga. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issurName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Återkallar certifikatet som identifieras av <span class="codeph"> utfärdarnamn</span> och <span class="codeph"> serienummer</span> på det angivna datumet. <span class="codeph"> utfärdarnamn</span> måste följa 509-namnformatet (till exempel <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Ange serienummer i hexadecimal form. Ange spärrdatumet som <span class="+ topic/ph pr-d/codeph codeph">ååå-mm-dd</span> eller <span class="+ topic/ph pr-d/codeph codeph">ååå-mm-dd-h24:min:sek</span>, till exempel 2008-12-1 eller 2008-12-1-00:00:00 för midnatt den 1, 2008. Om återkallningsdatumet inte anges används det aktuella datumet. </p> </td> 
  </tr> 
 </tbody> 
</table>

