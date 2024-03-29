---
title: Användning av kommandorad
description: Användning av kommandorad
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Användning av kommandorad {#command-line-usage}

Använd följande syntax när du bäddar in en licens:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` är en krypterad FLV- eller F4V-fil.
* `destfile` anger var det krypterade innehållet med den inbäddade licensen ska skrivas. Om en katalog anges sparas filen i den här katalogen med samma filnamn som källfilen, men katalogen får inte vara den katalog som innehåller källfilen.

I följande tabell beskrivs de kommandoradsalternativ som kan anges tillsammans med den tidigare nämnda syntaxen:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Namnet på filen som innehåller licensen som ska bäddas in. Flera <span class="codeph"> -l </span> kan anges för att bädda in flera licenser. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filnamn </span> </td> 
   <td colname="2" class="- topic/entry "> Ange de metadata för innehållet som en licens ska genereras för. (Krävs för att generera licens) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o </span> är inte inställt returneras ett fel. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns skriver du över den utan att fråga. </td> 
  </tr> 
 </tbody> 
</table>
