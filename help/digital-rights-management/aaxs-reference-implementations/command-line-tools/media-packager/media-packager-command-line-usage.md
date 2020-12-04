---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Kommandoradsanvändning {#command-line-usage}

Innan du använder Media Packager måste du se till att du uppfyller de krav som anges i Krav och att konfigurationsfilen innehåller den information som krävs (se konfigurationsfilen i *Använda referensimplementeringar för Adobe Access*.

Media Packager finns i katalogen [!DNL \Reference Implementation\Command Line tools] på dvd-skivan. Om du vill kryptera en enskild fil använder du följande syntax:

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` är filen som ska krypteras.
* `dest` Anger var det krypterade innehållet ska skrivas. Om en katalog anges sparas den krypterade filen i den här mappen med samma filnamn som källfilen, men katalogen får inte vara den katalog som innehåller källfilen.

Om du vill kryptera flera filer med samma nyckel (för stöd för flera bithastigheter) använder du följande syntax:

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` är en serie mellanrumsavgränsade källposter som representerar de filer som ska krypteras.
* `dest-directory` Anger var det krypterade innehållet ska skrivas. De krypterade filerna sparas i den här mappen med samma filnamn som källfilerna, men katalogen får inte vara den katalog som innehåller källfilerna.

Om du vill visa information om en krypterad fil använder du följande syntax:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` är den krypterade filen.

Om du vill visa information om en metadatafil använder du följande syntax:

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` är en  [!DNL .metadata] fil som innehåller DRM-metadata.

>[!NOTE]
>
>Under paketeringen genereras inte längre en .header-fil som standard. Om du vill generera den här filen använder du alternativet `-h` under paketeringen.

Följande tabell innehåller beskrivningar av kommandoradsalternativen som visas i syntaxen ovan:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Kommandoradsalternativ </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Beskrivning </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> konfigurationsfil </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger platsen för konfigurationsfilen. Om det här alternativet inte används söker Media Packager efter <span class="filepath"> flashaccesstools.properties </span> i arbetskatalogen. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> krypterad fil </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om en fil som redan har paketerats. Käll- och målfilerna är inte obligatoriska. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafil </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visar information om befintliga metadata. Käll- och målfilerna är inte obligatoriska. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd det här alternativet med <span class="codeph"> -d </span> för att extrahera principer från en paketerad fil. En fil skapas i samma katalog som den krypterade filen med hjälp av filnamnet och principidentifieraren. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd med <span class="codeph"> -d </span> för att extrahera DRM-huvudet från en paketerad fil. En fil skapas i samma katalog som den krypterade filen, med hjälp av filnamnet och tillägget <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger en unik identifierare för det här innehållet. Om ingen identifierare anges används målfilens namn. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> nyckel </span>= <span class="+ topic/ph pr-d/codeph codeph"> värde </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger en anpassad nyckel/värde som ska läggas till i innehållets metadata. Flera <span class="codeph"> -k </span>-alternativ kan anges. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Använd det här alternativet med <span class="codeph"> -d </span> för att extrahera metadata från en paketerad fil. En fil skapas i samma katalog som den krypterade filen med hjälp av filnamnet och tillägget <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Fråga inte om målfilen ska skrivas över. Om målfilen redan finns och <span class="codeph"> -o </span> inte har angetts returneras ett fel. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Skriver över målfilen utan att fråga, om den redan finns. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> filnamn [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger namnet på filen som innehåller profilen. Om principen kräver domänregistrering med en server som använder ett annat transportcertifikat än det som anges i egenskapsfilen, måste även domäntransportcertifikatet anges. </p> <p class="- topic/p ">Flera <span class="codeph"> -p </span>-alternativ kan anges, och klienten använder det första som standard. De värden som anges på kommandoraden har högre prioritet än de som anges i konfigurationsfilen. </p> </td> 
  </tr> 
 </tbody> 
</table>

