---
title: Bygg referensimplementeringen av BEES
description: Bygg referensimplementeringen av BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Bygg BES-referensimplementeringen {#build-the-bees-reference-implementation}

Kontrollera att du använder Java 1.6.0_24 eller senare.
1. Fyll i de tomma sökvägarna som behövs, till exempel `tomcatdir` och `fasterxmldir` i [!DNL build-bees.xml]

   FasterXML/Jackson ingår. Du kan även hämta den från [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Uppdatera filnamnen i den faktiska burken i [!DNL build.common.xml] om du vill använda en annan version av Jackson-biblioteken.
1. Kör `all`-målet för [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

[!DNL bees.war] skapas i mappen [!DNL bees-build/wars].