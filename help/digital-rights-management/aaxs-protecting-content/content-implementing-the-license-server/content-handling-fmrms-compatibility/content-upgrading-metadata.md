---
seo-title: Uppgraderar metadata
title: Uppgraderar metadata
uuid: cad0b23e-50ca-47ae-871f-be571cb00a26
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppgraderar metadata{#upgrading-metadata}

Om en Adobe Access-klient stöter på innehåll som paketerats med Flash Media Rights Management Server 1.x extraheras krypteringsmetadata från innehållet och skickas till servern. Servern konverterar FMRMS 1.x-metadata till Adobe Access-format och skickar tillbaka dem till klienten. Klienten skickar sedan de uppdaterade metadata i en standardbegäran om Adobe Access-licens.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

Metadatakonverteringen kan göras direkt när servern tar emot gamla metadata från klienten. Servern kan också förbearbeta det gamla innehållet och lagra de konverterade metadata. När klienten begär nya metadata behöver servern i det här fallet bara hämta nya metadata som matchar licensidentifieraren för de gamla metadata.

Servern måste utföra följande steg för att konvertera metadata:

* Gå `LiveCycleKeyMetaData`. Om du vill förkonvertera metadata kan du hämta dem från en 1.x-paketerad fil med `LiveCycleKeyMetaData` `MediaEncrypter.examineEncryptedContent()`. Metadata ingår också i begäran om konvertering av metadata ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Hämta licens-ID:t från gamla metadata och hitta krypteringsnyckeln och krypteringsprofilerna (den här informationen fanns ursprungligen i Adobe LiveCycle ES-databasen). LiveCycle ES-profilerna måste konverteras till Adobe Access 2.0-profiler.) Referensimplementeringen innehåller skript och exempelkod för konvertering av profiler och export av licensinformation från LiveCycle ES.
* Fyll i `V2KeyParameters` objektet (som du hämtar genom att anropa `MediaEncrypter.getKeyParameters()`).
* Läs in `SigningCredential`filen, som är den paketeringsautentisering som har utfärdats av Adobe och som används för att signera krypteringsmetadata. Hämta `SignatureParameters` objektet genom att anropa `MediaEncrypter.getSignatureParameters()` och fylla i signeringsinformationen.
* Ring `MetaDataConverter.convertMetadata()` för att få tillgång till `V2ContentMetaData`.
* Ring `V2ContentMetaData.getBytes()` och lagra för framtida bruk eller ring `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

