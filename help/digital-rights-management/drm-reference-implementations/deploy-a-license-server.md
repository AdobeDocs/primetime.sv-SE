---
title: Distribuera licensservern
description: Distribuera licensservern
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Distribuera licensservern{#deploy-the-license-server}

1. Kopiera referensimplementeringens krigsfiler till `webapps` på din Tomcat-server.

   Om du vill använda referensimplementeringslicensservern som den är kan du bara kopiera licensserverns WAR-fil ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) till `webapps` på din Tomcat-server.

   Om du anpassar referensimplementeringslicensservern kopierar du de server war-filer du har skapat från `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` till `webapps` katalog.

   >[!NOTE]
   >
   >Om du tidigare har distribuerat licensserverns WAR-filer kan du behöva ta bort de opackade WAR-katalogerna i [!DNL webapps] katalog på Tomcat-servern:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]

   >[!NOTE]
   >
   >Distribuera inte [!DNL edsws.war] såvida du inte behöver bakåtkompatibilitet med Flash Media Rights Management (FMRMS) v1.5-innehåll. (Detta är ett mycket sällsynt krav.)
   >
   >Om du föredrar att hindra Tomcat från att packa upp WAR-filer redigerar du `server.xml` i `conf` katalog och ange `unpackWARs` till `false`.

1. Kopiera hela innehållet i `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` till [!DNL tomcat] katalog.

   The [!DNL resources] katalogen innehåller:

   * [!DNL flashaccesstools.properties] - Licensserverns egenskapsfil.
   * [!DNL log4j.xml] - Loggningskonfiguration för licensserver
   * [!DNL *.pol] - Exempel på DRM-principfiler.

   Dessutom kan du välja att kopiera Adobe-certifieringsfilerna till den här platsen.

1. Ändra licensserverinställningarna i [!DNL flashaccesstools.properties] för att återspegla din serverkonfiguration.

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

1. Redigera `catalina.properties` i din Tomcat `conf` katalog; lägg till platsen för [!DNL resources] katalogen (eller den alternativa platsen där du har lagrat egenskapsfilen och andra resursfiler) till `shared.loader` -egenskap.

   Om du har `flashaccess-refimpl.properties` finns i [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Här finns `flashaccess-refimpl.properties` på klassökvägen.
1. Se till att dina andra resursfiler ( [!DNL log4j.xml], principfiler, certifieringar) finns antingen i [!DNL resources] eller finns på klassökvägen och den plats som anges i [!DNL flashaccess-refimpl.properties].

   Du vill förmodligen köra `log4j` i felsökningsläge. I [!DNL log4j.xml], ange `debug` till true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Från Tomcat [!DNL bin] -katalog, starta servern.

   I Linux:

   ```
   catalina.sh start
   ```

   I Windows:

   ```
   catalina.bat start
   ```
