---
title: Undersöker krypterat filinnehåll
description: Undersöker krypterat filinnehåll
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Undersöker krypterat filinnehåll {#examining-encrypted-file-content}

Så här undersöker du innehållet i en FLV- eller F4V-fil med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i [Konfigurera utvecklingsmiljön](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) i ditt projekt.
1. Skapa en `MediaEncrypter` -instans.
1. Skicka den krypterade filen till `MediaEncrypter.examineEncryptedContent` metod, som returnerar `KeyMetaData` -objekt.
1. Inspect the information within the `KeyMetaData` -objekt.

Exempelkod som visar hur du extraherar DRM-metadata från en krypterad fil finns i `com.adobe.flashaccess.samples.mediapackager.ExamineContent` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
