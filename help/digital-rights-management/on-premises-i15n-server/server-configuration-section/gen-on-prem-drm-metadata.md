---
title: Generera On Premises DRM-metadata
description: Generera On Premises DRM-metadata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Generera On Premises DRM-metadata{#generate-the-on-premises-drm-metadata}

Ett [!DNL CreateMetadata.jar]-verktyg finns i mappen [!DNL create_metadata]. Poängen med det här verktyget är att skapa en On Premises DRM-metadata som startar klienten att utföra personaliseringsprocessen mot den angivna On Premises Individualization Server.

1. Uppdatera implementeringen av DRM-referensen för Primetime - kommandoradsverktyg med följande filer:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      De två JAR-filerna kan finnas i mappen [!DNL Command Line Tools/libs]. Filen [!DNL createMetadata.properties] kan finnas bredvid filen [!DNL flashaccesstools.properties].

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Inkluderat är ett [!DNL examplecreate.sh]-skript som demonstrerar hur metadata skapas. Konfigurera licensserverns URL och URL:en till servern för personalisering i både skript- och egenskapsfilerna innan du försöker generera metadata.

Indata för verktyget är följande:

* `createMetadata.properties` - Egenskapsfil som innehåller en standardprofil, certifikatplatser och lösenord osv.
* `indivCert` - PKCS12-fil som innehåller individuellt transportcertifikat
* `indivURL` - URL för On Premises Individualization Server

Utdatafilen är en lokal DRM-metadatafil som ska användas av DRM-klienten. Exempel:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.