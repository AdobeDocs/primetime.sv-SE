---
description: Det finns två typer av förfrågningar relaterade till Flash Media Rights Management Server 1.x-kompatibilitet. En typ av begäran används för att uppmana 1.x-klienter att uppgradera till en körningsmiljö som stöder Adobe Primetime DRM 2.0 eller senare. Ett annat sätt används för att uppdatera 1.x-metadata till Primetimes DRM-format innan en licens kan begäras. Stöd för dessa förfrågningar behövs bara om du tidigare har distribuerat innehåll som använder FMRMS 1.0 eller 1.5.
seo-description: Det finns två typer av förfrågningar relaterade till Flash Media Rights Management Server 1.x-kompatibilitet. En typ av begäran används för att uppmana 1.x-klienter att uppgradera till en körningsmiljö som stöder Adobe Primetime DRM 2.0 eller senare. Ett annat sätt används för att uppdatera 1.x-metadata till Primetimes DRM-format innan en licens kan begäras. Stöd för dessa förfrågningar behövs bara om du tidigare har distribuerat innehåll som använder FMRMS 1.0 eller 1.5.
seo-title: Hantera FMRMS-kompatibilitet
title: Hantera FMRMS-kompatibilitet
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Hantera FMRMS-kompatibilitet {#handling-fmrms-compatibility}

Det finns två typer av förfrågningar relaterade till Flash Media Rights Management Server 1.x-kompatibilitet. En typ av begäran används för att uppmana 1.x-klienter att uppgradera till en körningsmiljö som stöder Adobe Primetime DRM 2.0 eller senare. Ett annat sätt används för att uppdatera 1.x-metadata till Primetimes DRM-format innan en licens kan begäras. Stöd för dessa förfrågningar behövs bara om du tidigare har distribuerat innehåll som använder FMRMS 1.0 eller 1.5.

## Uppgraderar klienter {#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Primetime DRM-server måste servern uppmana klienten att uppgradera.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Till skillnad från andra begärandehanterare för Adobe Primetime ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler`och anropa sedan `close()`

## Uppgraderar metadata {#upgrading-metadata}

Om en Adobe Primetime DRM-klient stöter på innehåll som paketerats med Flash Media Rights Management Server 1.x extraheras krypteringsmetadata från innehållet och skickas till servern. Servern konverterar sedan FMRMS 1.x-metadata till Primetimes DRM-format och skickar dem till klienten. Klienten skickar sedan de uppdaterade metadata i en standardbegäran om DRM-licens för Primetime.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

Metadatakonverteringen kan göras direkt när servern tar emot gamla metadata från klienten. Servern kan också förbearbeta det gamla innehållet och lagra de konverterade metadata. När klienten begär nya metadata behöver servern i det här fallet bara hämta nya metadata som matchar licensidentifieraren för de gamla metadata.

Servern måste utföra följande steg för att konvertera metadata:

* Gå `LiveCycleKeyMetaData`. Om du vill förkonvertera metadata kan du hämta dem från en 1.x-paketerad fil med `LiveCycleKeyMetaData` `MediaEncrypter.examineEncryptedContent()`. Metadata ingår också i begäran om konvertering av metadata ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Hämta licensidentifieraren från gamla metadata och hitta krypteringsnyckeln och DRM-profilerna (den här informationen fanns ursprungligen i Adobe LiveCycle ES-databasen). LiveCycle ES DRM-profilerna måste konverteras till DRM 2.0-principer för Primetime.) Referensimplementeringen innehåller skript och exempelkod för konvertering av DRM-profiler och export av licensinformation från LiveCycle ES.
* Fyll i `V2KeyParameters` objektet (som du hämtar genom att anropa `MediaEncrypter.getKeyParameters()`).

* Läs in `SigningCredential`filen, som är den paketeringsautentisering som har utfärdats av Adobe och som används för att signera krypteringsmetadata. Hämta `SignatureParameters` objektet genom att anropa `MediaEncrypter.getSignatureParameters()` och fylla i signeringsinformationen.

* Ring `MetaDataConverter.convertMetadata()` för att få tillgång till `V2ContentMetaData`.

* Ring `V2ContentMetaData.getBytes()` och lagra för framtida bruk eller ring `FMRMSv1MetadataHandler.setUpdatedMetadata()`.