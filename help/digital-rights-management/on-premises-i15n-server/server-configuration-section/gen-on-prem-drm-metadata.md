---
title: Generera On Premises DRM-metadata
description: Generera On Premises DRM-metadata
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Generera On Premises DRM-metadata{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] ingår i [!DNL create_metadata] mapp. Poängen med det här verktyget är att skapa en On Premises DRM-metadata som startar klienten att utföra personaliseringsprocessen mot den angivna On Premises Individualization Server.

1. Uppdatera implementeringen av DRM-referensen för Primetime - kommandoradsverktyg med följande filer:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     De två JAR-filerna kan finnas i [!DNL Command Line Tools/libs] mapp. The [!DNL createMetadata.properties] filen kan finnas bredvid [!DNL flashaccesstools.properties] -fil.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Inkluderad är en [!DNL examplecreate.sh] skript som demonstrerar hur metadata skapas. Konfigurera licensserverns URL och URL:en till servern för personalisering i både skript- och egenskapsfilerna innan du försöker generera metadata.

Indata för verktyget är följande:

* `createMetadata.properties` - Egenskapsfil som innehåller en standardprofil, certifikatplatser och lösenord osv.
* `indivCert` - PKCS12-fil som innehåller individuellt transportcertifikat
* `indivURL` - URL för On Premises Individualization Server

Utdatafilen är en lokal DRM-metadatafil som ska användas av DRM-klienten. Till exempel:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
