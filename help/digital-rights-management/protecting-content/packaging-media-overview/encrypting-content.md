---
title: Kryptera innehåll
description: Kryptera innehåll
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Kryptera innehåll{#encrypting-content}

Du krypterar videomaterial med `MediaEncrypter` -objekt. Du kan kryptera mediefiler som bara innehåller ljudspår. Du kan också bara tillämpa partiell kryptering, till exempel för att förbättra prestanda när du krypterar H.264-innehåll för enheter med lägre prestanda.

Så här krypterar du mediefiler med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i *Konfigurera utvecklingsmiljön* i ditt projekt.
1. Skapa en `ServerCredential` -instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter` -instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har.

1. Ange krypteringsalternativen med en `DRMParameters` -objekt.
1. Ange signaturalternativ med en `SignatureParameters` -objektet och skicka `ServerCredential` instans till dess `setServerCredentials` -metod.

1. Ange nyckel- och licensinformation med en `V2KeyParameters` -objekt. Ange DRM-principer med `setPolicies` -metod. Ange den information som klienten behöver för att kontakta licensservern genom att anropa `setLicenseServerUrl` och `setLicenseServerTransportCertificate` metoder. Ange krypteringsalternativen för CEK med hjälp av `setKeyProtectionOptions` och dess anpassade egenskaper med `setCustomProperties` -metod. Beroende på vilken typ av kryptering som används kan du slutligen `DRMKeyParameters` objekt till lämplig typ ( `VideoDRMParameters`, `AudioDRMParameters`) och ange krypteringsalternativ.

1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till `MediaEncrypter.encryptContent` -metod.

Exempelkod som visar hur du krypterar innehåll finns i `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i kommandoradsverktygen för referensimplementering [!DNL samples/] katalog.
