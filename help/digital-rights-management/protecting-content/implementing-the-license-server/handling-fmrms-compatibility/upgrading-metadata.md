---
seo-title: Uppgraderar metadata
title: Uppgraderar metadata
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Uppgraderar metadata{#upgrading-metadata}

Om en Adobe Primetime DRM-klient stöter på innehåll som paketerats med Flash Media Rights Management Server 1.x extraheras krypteringsmetadata från innehållet och skickas till servern. Servern konverterar sedan FMRMS 1.x-metadata till Primetimes DRM-format och skickar dem till klienten. Klienten skickar sedan de uppdaterade metadata i en standardbegäran om DRM-licens för Primetime.

* Begäranhanterarklassen är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x content*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

Metadatakonverteringen kan göras direkt när servern tar emot gamla metadata från klienten. Servern kan också förbearbeta det gamla innehållet och lagra de konverterade metadata. När klienten begär nya metadata behöver servern i det här fallet bara hämta nya metadata som matchar licensidentifieraren för de gamla metadata.

Servern måste utföra följande steg för att konvertera metadata:

* Hämta `LiveCycleKeyMetaData`. Om du vill förkonvertera metadata kan du hämta `LiveCycleKeyMetaData` från en 1.x-paketerad fil med `MediaEncrypter.examineEncryptedContent()`. Metadata ingår också i begäran om metadatakonvertering ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Hämta licensidentifieraren från gamla metadata och hitta krypteringsnyckeln och DRM-profiler (den här informationen fanns ursprungligen i Adobe LiveCycle ES-databasen. DRM-principerna för LiveCycle ES måste konverteras till DRM 2.0-DRM-principer för Primetime.) Referensimplementeringen innehåller skript och exempelkod för konvertering av DRM-policyer och export av licensinformation från LiveCycle ES.
* Fyll i `V2KeyParameters`-objektet (som du hämtar genom att anropa `MediaEncrypter.getKeyParameters()`).

* Läs in `SigningCredential`, som är den paketeringsautentisering som utfärdas av Adobe och som används för att signera krypteringsmetadata. Hämta `SignatureParameters`-objektet genom att anropa `MediaEncrypter.getSignatureParameters()` och fyll i signeringsreferensen.

* Ring `MetaDataConverter.convertMetadata()` för att hämta `V2ContentMetaData`.

* Ring `V2ContentMetaData.getBytes()` och lagra för framtida bruk eller ring `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

