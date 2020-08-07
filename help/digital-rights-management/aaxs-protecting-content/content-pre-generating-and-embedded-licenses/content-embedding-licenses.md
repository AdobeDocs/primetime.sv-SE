---
seo-title: Bädda in licenser
title: Bädda in licenser
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Bädda in licenser {#embedding-licenses}

När innehållet har krypterats och en licens har förgenererats kan licensen bäddas in i det krypterade innehållet.

Om du vill bädda in en licens hämtar du en instans av `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Om du vet vilken typ av krypterat innehåll det är använder du konstruktorn för `FLVKeyMetaDataUpdater` eller `F4VKeyMetaDataUpdater`; I annat fall använder du `MediaProcessorFactory.getMediaProcessor()` för att returnera en instans baserat på den upptäckta filtypen. Skapa en `KeyMetaDataCallback` och anropa `modifyKeyMetaData()`. Din återanropsimplementering anropas när DRM-metadata finns i det krypterade innehållet. Baserat på de metadata som hittas kan du välja vilken licens som ska bäddas in och ange licensen med `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Exempelkod som visar inbäddade licenser finns `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` i katalogen&quot;Exempel&quot; för kommandoradsverktygen för referensimplementering.

>[!NOTE]
>
>Adobe Access 2.0-klienter ignorerar alla licenser som är inbäddade i innehållet och försöker hämta en licens från den licensserver som anges i metadata. Om metadata anger att ingen licensserver är tillgänglig måste en Adobe Access 2.0-klient uppgradera för att kunna visa innehållet.

Se [Utökade licenser](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
