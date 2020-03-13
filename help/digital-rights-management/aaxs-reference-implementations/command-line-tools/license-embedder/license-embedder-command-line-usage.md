---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

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
   <td colname="2" class="- topic/entry "> Namnet på filen som innehåller licensen som ska bäddas in. Flera <span class="codeph"> -l- </span> alternativ kan anges för att bädda in flera licenser. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filnamn </span> </td> 
   <td colname="2" class="- topic/entry "> Ange de metadata för innehållet som en licens ska genereras för. (Krävs för att generera licens) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o inte </span> är inställd returneras ett fel. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns skriver du över den utan att fråga. </td> 
  </tr> 
 </tbody> 
</table>

