---
title: Undersöker krypterat filinnehåll
description: Undersöker krypterat filinnehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Undersöker krypterat filinnehåll {#examining-encrypted-file-content}

Så här undersöker du innehållet i en FLV- eller F4V-fil med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i [Konfigurera utvecklingsmiljön](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) i projektet.
1. Skapa en `MediaEncrypter`-instans.
1. Skicka den krypterade filen till metoden `MediaEncrypter.examineEncryptedContent`, som returnerar ett `KeyMetaData`-objekt.
1. Inspect informationen i `KeyMetaData`-objektet.

Exempelkod som visar hur du extraherar DRM-metadata från en krypterad fil finns i `com.adobe.flashaccess.samples.mediapackager.ExamineContent` i katalogen &quot;samples&quot; i Reference Implementation Command Line Tools.
