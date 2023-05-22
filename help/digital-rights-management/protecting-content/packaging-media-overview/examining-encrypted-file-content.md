---
title: Undersöker krypterat filinnehåll
description: Undersöker krypterat filinnehåll
copied-description: true
exl-id: df1fd04d-016e-4770-bcb9-97bfe2d39260
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
