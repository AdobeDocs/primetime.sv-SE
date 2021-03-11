---
title: Undersöker krypterat filinnehåll
description: Undersöker krypterat filinnehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Undersöker krypterat filinnehåll{#examining-encrypted-file-content}

Du kan granska innehållet i en krypterad mediefil med Java API.

Så här undersöker du krypterat filinnehåll:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer. Se *Konfigurera SDK* för ditt projekt.
1. Skapa en `MediaEncrypter`-instans.
1. Skicka den krypterade filen till metoden `MediaEncrypter.examineEncryptedContent`, som returnerar ett `KeyMetaData`-objekt.

1. Inspect informationen i `KeyMetaData`-objektet.

Exempelkod som beskriver hur du extraherar DRM-metadata från en krypterad fil finns i `com.adobe.flashaccess.samples.mediapackager.ExamineContent` i katalogen Reference Implementation Command Line Tools [!DNL samples/].
