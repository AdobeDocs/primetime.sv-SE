---
seo-title: Bygg referensimplementeringen av BEES
title: Bygg referensimplementeringen av BEES
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
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