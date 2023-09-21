---
title: Ökning
description: Ökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# DRM-licensinbäddning {#license-embedder}

Använd [!DNL AdobeLicenseEmbedder.jar] om du vill bädda in förgenererade licenser i innehåll som Media Packager skyddar.

## License Embedder-kommandoradsanvändning {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` representerar en krypterad fil.
* `destfile` Anger namnet på filen där det krypterade innehållet med den inbäddade licensen sparas.

  Om du anger en katalog sparas filen i målkatalogen. Namnet på källfilen blir också namnet på filen som sparas i målkatalogen.

I följande tabell beskrivs de kommandoradsalternativ som du kan ange:

**Tabell 7: Alternativ**

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
   <td colname="2" class="- topic/entry "> Namnet på filen som innehåller licensen som du vill bädda in. Du kan ange flera <span class="codeph"> -l </span> alternativ för att bädda in flera licenser. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filnamn </span> </td> 
   <td colname="2" class="- topic/entry "> Anger de innehållsmetadata som du kan generera en licens för. Det här alternativet krävs för att generera en licens. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o </span> har inte tillämpats, ett fel inträffar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns kan du skriva över den utan att tillfrågas. </td> 
  </tr> 
 </tbody> 
</table>
