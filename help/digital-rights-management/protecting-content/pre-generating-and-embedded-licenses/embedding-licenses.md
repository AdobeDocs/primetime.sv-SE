---
title: Bädda in licenser
description: Bädda in licenser
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Bädda in licenser {#embedding-licenses}

När innehållet har krypterats och en licens har förgenererats kan licensen bäddas in i det krypterade innehållet.

Om du vill bädda in en licens måste du skaffa en instans av `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Om du vet vilken typ av krypterat innehåll det är använder du konstruktorn för `FLVKeyMetaDataUpdater` eller `F4VKeyMetaDataUpdater`; I annat fall använder du `MediaProcessorFactory.getMediaProcessor()` för att returnera en instans baserat på den upptäckta filtypen. Sedan måste du konstruera en `KeyMetaDataCallback` och anropa `modifyKeyMetaData()`. Din återanropsimplementering anropas sedan när DRM-metadata finns i det krypterade innehållet. Baserat på de metadata som hittats kan du välja en licens att bädda in och ange licensen med `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Se `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` i katalogen Reference Implementation Command Line Tools [!DNL Samples] för exempelkod som demonstrerar inbäddade licenser.

>[!NOTE]
>
>En Adobe Primetime DRM 2.0-klient ignorerar alla licenser som är inbäddade i innehållet och försöker sedan hämta en licens från licensservern som anges i metadata. Om metadata anger att ingen licensserver är tillgänglig måste en Primetime DRM 2.0-klient uppgraderas innan du kan visa innehållet.

