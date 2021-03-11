---
title: Kryptera innehåll
description: Kryptera innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Krypterar innehåll{#encrypting-content}

När du krypterar FLV- och F4V-innehåll används ett `MediaEncrypter`-objekt. Du kan också paketera FLV- och F4V-filer som bara innehåller ljudspår. När du krypterar H.264-innehåll för enheter med lägre prestanda kan det vara praktiskt att endast tillämpa partiell kryptering för att förbättra prestandan. I sådana fall kan en F4V-fil delvis krypteras med metoden `F4VDRMParameters.setVideoEncryptionLevel`.

Så här krypterar du en FLV- eller F4V-fil med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i Konfigurera utvecklingsmiljön i ditt projekt.
1. Skapa en `ServerCredential`-instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `MediaEncrypter`-instans. Använd en `MediaEncryperFactory` om du inte vet vilken typ av fil du har. Annars kan du skapa en `FLVEncrypter` eller `F4VEncrypter` direkt.
1. Ange krypteringsalternativen med ett `DRMParameters`-objekt.
1. Ange signaturalternativen med ett `SignatureParameters`-objekt och skicka `ServerCredential`-instansen till dess `setServerCredentials`-metod.
1. Ange nyckel- och licensinformation med ett `V2KeyParameters`-objekt. Ange profilerna med metoden `setPolicies`. Ange den information som klienten behöver för att kontakta licensservern genom att anropa metoderna `setLicenseServerUrl` och `setLicenseServerTransportCertificate`. Ange krypteringsalternativen för CEK med metoden `setKeyProtectionOptions` och dess anpassade egenskaper med metoden `setCustomProperties`. Beroende på vilken typ av kryptering som används konverterar du `DRMKeyParameters`-objektet till `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` eller `F4VDRMParameters` och anger krypteringsalternativen.
1. Kryptera innehållet genom att skicka in- och utdatafilerna samt krypteringsalternativen till metoden `MediaEncrypter.encryptContent`.

Exempelkod som visar hur du krypterar innehåll finns i `com.adobe.flashaccess.samples.mediapackager.EncryptContent` i katalogen &quot;samples&quot; i Command Line Tools för Reference Implementation.
