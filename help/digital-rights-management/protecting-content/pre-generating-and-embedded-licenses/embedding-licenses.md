---
seo-title: Bädda in licenser
title: Bädda in licenser
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Bädda in licenser {#embedding-licenses}

När innehållet har krypterats och en licens har förgenererats kan licensen bäddas in i det krypterade innehållet.

Om du vill bädda in en licens måste du skaffa en instans av `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Om du vet vilken typ av krypterat innehåll det är använder du konstruktorn för `FLVKeyMetaDataUpdater` eller `F4VKeyMetaDataUpdater`; I annat fall använder du `MediaProcessorFactory.getMediaProcessor()` för att returnera en instans baserat på den upptäckta filtypen. Sedan måste du konstruera en `KeyMetaDataCallback` och anropa `modifyKeyMetaData()`. Din återanropsimplementering anropas sedan när DRM-metadata finns i det krypterade innehållet. Baserat på de metadata som hittas kan du välja vilken licens som ska bäddas in och ange licensen med `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

I `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` katalogen Reference Implementation Command Line Tools finns [!DNL Samples] exempelkod som demonstrerar inbäddade licenser.

>[!NOTE]
>
>En Adobe Primetime DRM 2.0-klient ignorerar alla licenser som är inbäddade i innehållet och försöker sedan hämta en licens från licensservern som anges i metadata. Om metadata anger att ingen licensserver är tillgänglig måste en Primetime DRM 2.0-klient uppgraderas innan du kan visa innehållet.

