---
seo-title: Kryptera innehåll
title: Kryptera innehåll
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Krypterar innehåll{#encrypting-content}

Du krypterar videoinnehåll med objektet `MediaEncrypter`. Du kan kryptera mediefiler som bara innehåller ljudspår. Du kan också endast tillämpa partiell kryptering; till exempel för att förbättra prestanda när du krypterar H.264-innehåll för enheter med lägre prestanda.

Så här krypterar du mediefiler med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i *Konfigurera utvecklingsmiljön* i projektet.
1. Skapa en `ServerCredential`-instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter`-instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har.

1. Ange krypteringsalternativen med ett `DRMParameters`-objekt.
1. Ange signaturalternativen med ett `SignatureParameters`-objekt och skicka `ServerCredential`-instansen till dess `setServerCredentials`-metod.

1. Ange nyckel- och licensinformation med ett `V2KeyParameters`-objekt. Ange DRM-principer med metoden `setPolicies`. Ange den information som klienten behöver för att kontakta licensservern genom att anropa metoderna `setLicenseServerUrl` och `setLicenseServerTransportCertificate`. Ange krypteringsalternativen för CEK med metoden `setKeyProtectionOptions` och dess anpassade egenskaper med metoden `setCustomProperties`. Beroende på vilken typ av kryptering som används konverterar du `DRMKeyParameters`-objektet till lämplig typ ( `VideoDRMParameters`, `AudioDRMParameters`) och anger krypteringsalternativen.

1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till metoden `MediaEncrypter.encryptContent`.

Exempelkod som visar hur du krypterar innehåll finns i `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i katalogen Reference Implementation Command Line Tools [!DNL samples/].
