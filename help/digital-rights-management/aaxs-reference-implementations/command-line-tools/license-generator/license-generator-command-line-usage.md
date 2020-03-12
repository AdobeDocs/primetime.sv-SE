---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: b3a995de-653e-491a-9262-86dc56b9ce31
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Användning av kommandorad {#command-line-usage}

Använd följande syntax för att generera en licens:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` är en .metadata-fil som innehåller DRM-metadata för Adobe Access. Den här filen kan hämtas från skyddat innehåll med `-d -m` alternativet Media Packager.

Om du vill visa en tidigare genererad licens använder du följande syntax:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` är en fil som innehåller en Adobe Access-licens som genereras av licensgeneratorn.

I följande tabell beskrivs de kommandoradsalternativ som kan anges tillsammans med den tidigare nämnda syntaxen:

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
   <td colname="2" class="- topic/entry "> Ange platsen för konfigurationsfilen. Om det här alternativet inte används söker licensgeneratorn efter flashaccesstools.properties i arbetskatalogen. De alternativ som anges på kommandoraden har företräde framför de som finns i konfigurationsfilen. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensfil</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Visa information om en licens som redan har skapats. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Generera en lövlicens och skriv utdata till en angiven fil. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filnamn</span> </td> 
   <td colname="2" class="- topic/entry "> Ange de metadata för innehållet som en licens ska genereras för. (Krävs för att generera licens) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o</span> inte är inställd returneras ett fel. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Om målfilen redan finns skriver du över den utan att fråga. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Om metadata innehåller flera profiler anger du numret på profilen som ska användas (med början vid 1) för att generera licensen. Om inget anges används den första principen. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r mottagare-cert</span> </td> 
   <td colname="2" class="- topic/entry ">Generera en licens för den angivna mottagaren. Ett enhets- eller domäncertifikat kan användas. Flera <span class="+ topic/ph pr-d/codeph codeph"> -r- </span>alternativ kan anges för att skapa en licens för flera mottagare. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Generera en rotlicens och skriv utdata till den angivna filen. </td> 
  </tr> 
 </tbody> 
</table>

