---
description: Det finns två typer av förfrågningar relaterade till kompatibiliteten Flash Media Rights Management Server 1.x. En typ av begäran används för att uppmana 1.x-klienter att uppgradera till en runtime som stöder Adobe Primetime DRM 2.0 eller senare. Ett annat sätt används för att uppdatera 1.x-metadata till Primetimes DRM-format innan en licens kan begäras. Stöd för dessa förfrågningar behövs bara om du tidigare har distribuerat innehåll som använder FMRMS 1.0 eller 1.5.
title: Hantera FMRMS-kompatibilitet
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Hantera FMRMS-kompatibilitet {#handling-fmrms-compatibility}

Det finns två typer av förfrågningar relaterade till kompatibiliteten Flash Media Rights Management Server 1.x. En typ av begäran används för att uppmana 1.x-klienter att uppgradera till en runtime som stöder Adobe Primetime DRM 2.0 eller senare. Ett annat sätt används för att uppdatera 1.x-metadata till Primetimes DRM-format innan en licens kan begäras. Stöd för dessa förfrågningar behövs bara om du tidigare har distribuerat innehåll som använder FMRMS 1.0 eller 1.5.

## Uppgraderar klienter {#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Primetime DRM-server måste servern uppmana klienten att uppgradera.

* Begäranhanterarklassen är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x content*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Till skillnad från andra begärandehanterare för Adobe Primetime ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler` och anropa sedan `close()`

## Uppgraderar metadata {#upgrading-metadata}

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