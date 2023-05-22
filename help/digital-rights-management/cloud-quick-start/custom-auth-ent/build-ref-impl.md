---
title: Bygg referensimplementeringen av BEES
description: Bygg referensimplementeringen av BEES
copied-description: true
exl-id: 330c14de-fe4e-4cc8-b0a5-8f7c74417adf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Bygg referensimplementeringen av BEES {#build-the-bees-reference-implementation}

Kontrollera att du använder Java 1.6.0_24 eller senare.
1. Fyll i tomma banor som behövs, till exempel `tomcatdir` och `fasterxmldir` in [!DNL build-bees.xml]

   FasterXML/Jackson ingår. Du kan även hämta den från [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Uppdatera riktiga jar-filnamn i [!DNL build.common.xml] om du vill använda en annan version av Jackson-biblioteken.
1. Kör `all` mål för [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

The [!DNL bees.war] skapas i [!DNL bees-build/wars] mapp.
