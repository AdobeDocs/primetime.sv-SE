---
title: Kryptera innehåll
description: Kryptera innehåll
copied-description: true
exl-id: 84a490ae-af0c-43c5-a849-ed832e83a28d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Kryptera innehåll{#encrypting-content}

När du krypterar FLV- och F4V-innehåll används en `MediaEncrypter` -objekt. Du kan också paketera FLV- och F4V-filer som bara innehåller ljudspår. När du krypterar H.264-innehåll för enheter med lägre prestanda kan det vara praktiskt att endast tillämpa partiell kryptering för att förbättra prestandan. I sådana fall kan en F4V-fil krypteras delvis med `F4VDRMParameters.setVideoEncryptionLevel`-metod.

Så här krypterar du en FLV- eller F4V-fil med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i Konfigurera utvecklingsmiljön i ditt projekt.
1. Skapa en `ServerCredential` -instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter` -instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har. I annat fall kan du skapa en `FLVEncrypter` eller `F4VEncrypter` direkt.
1. Ange krypteringsalternativen med en `DRMParameters` -objekt.
1. Ange signaturalternativ med en `SignatureParameters` -objektet och skicka `ServerCredential` instans till `setServerCredentials` -metod.
1. Ange nyckel- och licensinformation med en `V2KeyParameters` -objekt. Ange profiler med hjälp av `setPolicies` -metod. Ange den information klienten behöver för att kontakta licensservern genom att anropa `setLicenseServerUrl` och `setLicenseServerTransportCertificate` metoder. Ange krypteringsalternativen för CEK med hjälp av `setKeyProtectionOptions` och dess anpassade egenskaper med `setCustomProperties` -metod. Beroende på vilken typ av kryptering som används kan du slutligen `DRMKeyParameters` objekt till något av `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`, eller `F4VDRMParameters`och ange krypteringsalternativ.
1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till `MediaEncrypter.encryptContent` -metod.

Exempelkod som visar hur du krypterar innehåll finns i `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
