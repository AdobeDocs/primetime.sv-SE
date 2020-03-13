---
seo-title: Generera On Premises DRM-metadata
title: Generera On Premises DRM-metadata
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generera On Premises DRM-metadata{#generate-the-on-premises-drm-metadata}

Ett [!DNL CreateMetadata.jar] verktyg finns i [!DNL create_metadata] mappen. Poängen med det här verktyget är att skapa en On Premises DRM-metadata som startar klienten att utföra personaliseringsprocessen mot den angivna On Premises Individualization Server.

1. Uppdatera implementeringen av DRM-referensen för Primetime - kommandoradsverktyg med följande filer:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      De två JAR-filerna kan finnas i [!DNL Command Line Tools/libs] mappen. Filen kan [!DNL createMetadata.properties] finnas bredvid [!DNL flashaccesstools.properties] filen.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Inkluderat är ett [!DNL examplecreate.sh] skript som demonstrerar hur metadata skapas. Konfigurera licensserverns URL och URL:en till servern för personalisering i både skript- och egenskapsfilerna innan du försöker generera metadata.

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