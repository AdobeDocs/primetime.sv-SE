---
title: Distribuera licensservern
description: Distribuera licensservern
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Distribuera licensservern{#deploy-the-license-server}

1. Kopiera dina referensimplementeringsfiler till katalogen `webapps` på din Tomcat-server.

   Om du vill använda referensimplementeringslicensservern som den är kan du bara kopiera licensserverns WAR-fil ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) till katalogen `webapps` på Tomcat-servern.

   Om du anpassar referensimplementeringslicensservern kopierar du de serverkrigsfiler du har skapat från `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` till katalogen `webapps`.

   >[!NOTE]
   >
   >Om du tidigare har distribuerat licensserverns WAR-filer kan du behöva ta bort de opackade WAR-katalogerna i katalogen [!DNL webapps] på Tomcat-servern:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Distribuera inte [!DNL edsws.war] om du inte behöver bakåtkompatibilitet med FMRMS v1.5-innehåll (Flash Media Rights Management). (Detta är ett mycket sällsynt krav.)
   >
   >Om du föredrar att hindra Tomcat från att packa upp WAR-filer redigerar du `server.xml` i katalogen `conf` och anger `unpackWARs` till `false`.

1. Kopiera hela innehållet i `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\`-katalogen till [!DNL tomcat]-katalogen.

   Katalogen [!DNL resources] innehåller:

   * [!DNL flashaccesstools.properties] - Licensserverns egenskapsfil.
   * [!DNL log4j.xml] - Loggningskonfiguration för licensserver
   * [!DNL *.pol] - Exempel på DRM-principfiler.

   Dessutom kan du välja att kopiera Adobe-certifieringsfilerna till den här platsen.

1. Ändra licensserverinställningarna i [!DNL flashaccesstools.properties] så att de återspeglar serverkonfigurationen.

   Ange minst värden för följande egenskaper:

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. Redigera `catalina.properties`-filen i din Tomcat `conf`-katalog; lägg till platsen för din [!DNL resources]-katalog (eller den alternativa platsen där du har lagrat egenskapsfilen och andra resursfiler) till egenskapen `shared.loader`.

   Om du till exempel har `flashaccess-refimpl.properties` i [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Detta placerar `flashaccess-refimpl.properties` i klassökvägen.
1. Kontrollera att dina andra resursfiler ( [!DNL log4j.xml], principfiler, certifieringar) antingen finns i katalogen [!DNL resources] eller på annat sätt finns i klassökvägen och deras plats som anges i [!DNL flashaccess-refimpl.properties].

   Du vill förmodligen initialt köra `log4j` i felsökningsläge. I [!DNL log4j.xml] anger du `debug` till true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Starta servern i Tomcat-katalogen [!DNL bin].

   I Linux:

   ```
   catalina.sh start
   ```

   I Windows:

   ```
   catalina.bat start
   ```
