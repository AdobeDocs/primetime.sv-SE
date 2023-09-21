---
description: Använd funktionen Extern CEK för att leverera och paketera licenser med din befintliga CKMS.
title: Använda externt CEK för att sälja och paketera licenser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Använda externt CEK för att sälja och paketera licenser{#using-external-cek-to-vend-and-package-licenses}

Använd funktionen Extern CEK för att leverera och paketera licenser med din befintliga CKMS.

## EncryptContentWithExternalKey.java

Detta är ett kommandoradsverktyg som AAXS-krypterar en video och skapar metadata som *not* innehåller CEK (skyddat med en AXS-licensservers offentliga certifikat). Verktyget bäddar i stället in ett CEK-ID i videons metadata.

Vid licensköp observerar AXS-licensservern en flagga i metadata som identifierar att innehållet har skyddats med en extern CEK. Licensservern extraherar CEK-ID från metadata och frågar sedan en säker databas/CKMS för att hämta rätt CEK.

## Paketeringsarbetsflöde

1. Kontrollera att du använder Java 1.6.0_24 eller senare.
1. Så här ser du hur verktyget används: `java -jar AdobePackager_ExternalCEK.jar`
1. Så här paketerar du innehåll:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Java-källkoden kan byggas med den medföljande ANT-koden `build-samples.xml`
>* Flash Access-SDK ( `adobe-flashaccess-sdk.jar`) måste finnas i klassökvägen
>

## Serverarbetsflöde

1. Konfigurera referensimplementeringen.
1. Om det finns några, rensa upp tidigare distributioner av referensimplementering:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifiera att det finns en [!DNL CEKDepot.properties] -filen tillsammans med [!DNL flashaccess-refimpl.properties]

1. Initiera en licensbegäran från en Adobe Primetime Player
1. Observera Ref Impl-loggar för något liknande:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Du kan behöva ändra din [!DNL log4j.xml] inställningar för att logga in på `DEBUG` level ( `INFO` är inställd som standard)

## Kända fel

Ingen
