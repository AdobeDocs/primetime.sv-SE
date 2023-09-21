---
title: Undersöker krypterat filinnehåll
description: Undersöker krypterat filinnehåll
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Undersöker krypterat filinnehåll{#examining-encrypted-file-content}

Du kan granska innehållet i en krypterad mediefil med Java API.

Så här undersöker du krypterat filinnehåll:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer. Se *Konfigurera SDK* för ditt projekt.
1. Skapa en `MediaEncrypter` -instans.
1. Skicka den krypterade filen till `MediaEncrypter.examineEncryptedContent` metod, som returnerar `KeyMetaData` -objekt.

1. Inspect the information within the `KeyMetaData` -objekt.

Exempelkod som beskriver hur du extraherar DRM-metadata från en krypterad fil finns i `com.adobe.flashaccess.samples.mediapackager.ExamineContent` i kommandoradsverktygen för referensimplementering [!DNL samples/] katalog.
