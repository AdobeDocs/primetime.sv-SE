---
seo-title: Kryptera innehåll
title: Kryptera innehåll
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Kryptera innehåll{#encrypting-content}

När du krypterar FLV- och F4V-innehåll används ett `MediaEncrypter` objekt. Du kan också paketera FLV- och F4V-filer som bara innehåller ljudspår. När du krypterar H.264-innehåll för enheter med lägre prestanda kan det vara praktiskt att endast tillämpa partiell kryptering för att förbättra prestandan. I sådana fall kan en F4V-fil krypteras delvis med `F4VDRMParameters.setVideoEncryptionLevel`metoden .

Så här krypterar du en FLV- eller F4V-fil med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i Konfigurera utvecklingsmiljön i ditt projekt.
1. Skapa en `ServerCredential` instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter` instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har. I annat fall kan du skapa en `FLVEncrypter` eller `F4VEncrypter` direkt.
1. Ange krypteringsalternativen med hjälp av ett `DRMParameters` objekt.
1. Ange signaturalternativen med ett `SignatureParameters` objekt och skicka `ServerCredential` instansen till dess `setServerCredentials` metod.
1. Ange nyckel- och licensinformation med hjälp av ett `V2KeyParameters` objekt. Ange profilerna med `setPolicies` metoden . Ange den information som klienten behöver för att kontakta licensservern genom att anropa metoderna `setLicenseServerUrl` och `setLicenseServerTransportCertificate` . Ange krypteringsalternativen för CEK med hjälp av `setKeyProtectionOptions` metoden och dess anpassade egenskaper med hjälp av `setCustomProperties` metoden. Beroende på vilken typ av kryptering som används kan du slutligen omvandla `DRMKeyParameters` objektet till något av `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`eller `F4VDRMParameters`, och ange krypteringsalternativen.
1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till `MediaEncrypter.encryptContent` metoden.

Exempelkod som visar hur du krypterar innehåll finns `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i katalogen&quot;samples&quot; i Command Line Tools för Reference Implementation.
