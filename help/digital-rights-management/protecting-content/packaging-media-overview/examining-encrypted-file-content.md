---
seo-title: Undersöker krypterat filinnehåll
title: Undersöker krypterat filinnehåll
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Undersöker krypterat filinnehåll{#examining-encrypted-file-content}

Du kan granska innehållet i en krypterad mediefil med Java API.

Så här undersöker du krypterat filinnehåll:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer. Se *Konfigurera SDK* för ditt projekt.
1. Skapa en `MediaEncrypter` instans.
1. Skicka den krypterade filen till `MediaEncrypter.examineEncryptedContent` metoden som returnerar ett `KeyMetaData` objekt.

1. Granska informationen i `KeyMetaData` objektet.

Exempelkod som beskriver hur du extraherar DRM-metadata från en krypterad fil finns `com.adobe.flashaccess.samples.mediapackager.ExamineContent` i [!DNL samples/] katalogen Reference Implementation Command Line Tools.
