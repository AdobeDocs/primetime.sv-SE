---
title: Bädda in licenser
description: Bädda in licenser
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Bädda in licenser {#embedding-licenses}

När innehållet har krypterats och en licens har förgenererats kan licensen bäddas in i det krypterade innehållet.

Om du vill bädda in en licens hämtar du en instans av `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Om du vet vilken typ av krypterat innehåll det är använder du konstruktorn för `FLVKeyMetaDataUpdater` eller `F4VKeyMetaDataUpdater`, annars används `MediaProcessorFactory.getMediaProcessor()` för att returnera en instans baserat på den upptäckta filtypen. Skapa en `KeyMetaDataCallback` och anropa `modifyKeyMetaData()`. Din återanropsimplementering anropas när DRM-metadata finns i det krypterade innehållet. Baserat på de metadata som hittats kan du välja vilken licens som ska bäddas in och ange licensen med `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Exempelkod som visar inbäddade licenser finns i `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` i katalogen &quot;Samples&quot; i kommandoraden för referensimplementering.

>[!NOTE]
>
>Adobe Access 2.0-klienter ignorerar alla licenser som är inbäddade i innehållet och försöker hämta en licens från den licensserver som anges i metadata. Om metadata anger att ingen licensserver är tillgänglig måste en Adobe Access 2.0-klient uppgradera för att kunna visa innehållet.

Se [Out-of-band-licenser](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
