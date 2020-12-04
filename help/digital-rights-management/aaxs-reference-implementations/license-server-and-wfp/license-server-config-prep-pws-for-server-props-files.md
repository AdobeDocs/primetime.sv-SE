---
seo-title: Förbereda lösenord för serveregenskapsfiler
title: Förbereda lösenord för serveregenskapsfiler
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Förbereder lösenord för serveregenskapsfilerna {#preparing-passwords-for-the-server-properties-files}

För att säkerställa säkerheten för autentiseringsuppgiftens lösenord finns det ett verktyg för att kryptera lösenordet innan det anges i [!DNL flashaccess-refimpl.properties]- eller [!DNL flashaccess-refimpl-packager.properties]-filen.

Så här kör du verktyget med det ANT-skript som finns:

* Gå till *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Kontrollera att egenskapen `sdkdir` i [!DNL build-refimpl.xml] pekar på katalogen som innehåller Adobe Access SDK
* Kör följande kommando med ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Skriv inloggningsuppgiftens lösenord när du uppmanas till det

Så här kör du verktyget med Java:

* Gå till *`<Reference Implementation Server Path>`*\[!DNL scrambler]

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
