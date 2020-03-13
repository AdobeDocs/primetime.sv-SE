---
description: 'null'
seo-description: 'null'
seo-title: Distribuera licensservern
title: Distribuera licensservern
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# Distribuera licensservern{#deploy-the-license-server}

1. Kopiera dina referensimplementeringskrigsfiler till `webapps` katalogen på din Tomcat-server.

   Om du vill använda referensimplementeringslicensservern som den är kan du bara kopiera licensserverns WAR-fil ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) till `webapps` katalogen på Tomcat-servern.

   Om du anpassar referensimplementeringslicensservern kopierar du de server war-filer du har skapat från `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` till `webapps` katalogen.

   >[!NOTE]
   >
   >Om du tidigare har distribuerat licensserverns WAR-filer kan du behöva ta bort de opackade WAR-katalogerna i [!DNL webapps] katalogen på Tomcat-servern:        >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Distribuera inte [!DNL edsws.war] såvida du inte behöver bakåtkompatibilitet med FMRMS v1.5-innehåll (Flash Media Rights Management). (Detta är ett mycket sällsynt krav.)
   >
   >Om du föredrar att hindra Tomcat från att packa upp WAR-filer redigerar du `server.xml` i `conf` katalogen och anger `unpackWARs` till `false`.

1. Kopiera allt innehåll i `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` katalogen till din [!DNL tomcat] katalog.

   Katalogen innehåller [!DNL resources] :

   * [!DNL flashaccesstools.properties] - Licensserverns egenskapsfil.
   * [!DNL log4j.xml] - Loggningskonfiguration för licensserver
   * [!DNL *.pol] - Exempel på DRM-principfiler.
   Dessutom kan du välja att kopiera Adobes certifieringsfiler till den här platsen.

1. Ändra licensserverinställningarna i [!DNL flashaccesstools.properties] för att återspegla serverkonfigurationen.

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

1. Redigera `catalina.properties` filen i din Tomcat- `conf` katalog; lägg till platsen för din [!DNL resources] katalog (eller den alternativa platsen där du har lagrat egenskapsfilen och andra resursfiler) till `shared.loader` egenskapen.

   Om du till exempel har `flashaccess-refimpl.properties` besökt [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Det här placerar `flashaccess-refimpl.properties` i klassökvägen.
1. Kontrollera att dina andra resursfiler ( [!DNL log4j.xml]principfiler, certifieringar) antingen finns i [!DNL resources] katalogen eller på annat sätt finns i klassökvägen och deras plats som anges i [!DNL flashaccess-refimpl.properties].

   Du vill antagligen köra `log4j` i felsökningsläge från början. In [!DNL log4j.xml], set `debug` to true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Starta servern från Tomcat- [!DNL bin] katalogen.

   I Linux:

   ```
   catalina.sh start
   ```

   I Windows:

   ```
   catalina.bat start
   ```
