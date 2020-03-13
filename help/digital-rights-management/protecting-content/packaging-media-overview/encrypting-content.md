---
seo-title: Kryptera innehåll
title: Kryptera innehåll
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Kryptera innehåll{#encrypting-content}

Du krypterar videoinnehåll med `MediaEncrypter` objektet. Du kan kryptera mediefiler som bara innehåller ljudspår. Du kan också endast tillämpa partiell kryptering; till exempel för att förbättra prestanda när du krypterar H.264-innehåll för enheter med lägre prestanda.

Så här krypterar du mediefiler med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i *Konfigurera utvecklingsmiljön* i ditt projekt.
1. Skapa en `ServerCredential` instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter` instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har.

1. Ange krypteringsalternativen med hjälp av ett `DRMParameters` objekt.
1. Ange signaturalternativen med ett `SignatureParameters` objekt och skicka `ServerCredential` instansen till dess `setServerCredentials` metod.

1. Ange nyckel- och licensinformation med hjälp av ett `V2KeyParameters` objekt. Ange DRM-principer med `setPolicies` metoden . Ange den information som klienten behöver för att kontakta licensservern genom att anropa metoderna `setLicenseServerUrl` och `setLicenseServerTransportCertificate` . Ange krypteringsalternativen för CEK med hjälp av `setKeyProtectionOptions` metoden och dess anpassade egenskaper med hjälp av `setCustomProperties` metoden. Beroende på vilken typ av kryptering som används kan du slutligen omvandla objektet till rätt typ ( `DRMKeyParameters` , `VideoDRMParameters``AudioDRMParameters`) och ange krypteringsalternativen.

1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till `MediaEncrypter.encryptContent` metoden.

Exempelkod som visar hur du krypterar innehåll finns `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i [!DNL samples/] katalogen Reference Implementation Command Line Tools.
