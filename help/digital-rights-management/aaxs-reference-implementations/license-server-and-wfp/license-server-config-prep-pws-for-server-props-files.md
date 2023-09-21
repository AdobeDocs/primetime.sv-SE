---
title: Förbereda lösenord för serveregenskapsfiler
description: Förbereda lösenord för serveregenskapsfiler
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Förbereda lösenord för serveregenskapsfiler {#preparing-passwords-for-the-server-properties-files}

För att säkerställa säkerheten för inloggningsuppgiftens lösenord finns det ett verktyg som krypterar lösenordet innan det anges i [!DNL flashaccess-refimpl.properties] eller [!DNL flashaccess-refimpl-packager.properties] -fil.

Så här kör du verktyget med det ANT-skript som finns:

* Gå till *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Kontrollera `sdkdir` egenskap i [!DNL build-refimpl.xml] pekar på katalogen som innehåller Adobe Access SDK
* Kör följande kommando med ANT:

  ```
      ant -f build-refimpl.xml
  ```

* Skriv inloggningsuppgiftens lösenord när du uppmanas till det

Så här kör du verktyget med Java:

* Gå till *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* Ange kommandot från kommandotolken:

* I Windows:

  ```
  java -classpath path_to_adobe-flashaccess-sdk.jar;.  
  com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

* I Linux:

  ```
      java -classpath path_to_adobe-flashaccess-sdk.jar;.  
      com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

Verktyget matar ut det krypterade lösenordet, som du måste kopiera till .properties-filen.

>[!NOTE]
>
>Lösenord som är kodade med verktyget för lösenordskryptering som ingår i referensimplementeringen fungerar inte med Adobe Access Server för skyddad strömning.
