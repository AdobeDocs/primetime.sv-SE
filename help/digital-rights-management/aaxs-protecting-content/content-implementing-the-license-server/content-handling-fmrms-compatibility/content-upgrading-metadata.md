---
title: Uppgraderar metadata
description: Uppgraderar metadata
copied-description: true
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Uppgraderar metadata{#upgrading-metadata}

Om en Adobe Access-klient stöter på innehåll som paketerats med Flash Media Rights Management Server 1.x extraheras krypteringsmetadata från innehållet och skickas till servern. Servern konverterar FMRMS 1.x-metadata till Adobe Access-format och skickar tillbaka dem till klienten. Klienten skickar sedan de uppdaterade metadata som en standardbegäran om Adobe Access-licens.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

Metadatakonverteringen kan göras direkt när servern tar emot gamla metadata från klienten. Servern kan också förbearbeta det gamla innehållet och lagra de konverterade metadata. När klienten begär nya metadata behöver servern i det här fallet bara hämta nya metadata som matchar licensidentifieraren för de gamla metadata.

Servern måste utföra följande steg för att konvertera metadata:

* Hämta `LiveCycleKeyMetaData`. Om du vill konvertera metadata i förväg `LiveCycleKeyMetaData` kan hämtas från en 1.x-paketerad fil med `MediaEncrypter.examineEncryptedContent()`. Metadata ingår också i begäran om metadatakonvertering ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Hämta licensidentifieraren från gamla metadata och hitta krypteringsnyckeln och krypteringsprofilerna (den här informationen fanns ursprungligen i Adobe LiveCycle ES-databasen. LiveCycle ES-profilerna måste konverteras till Adobe Access 2.0-profilerna.) Referensimplementeringen innehåller skript och exempelkod för konvertering av policyer och export av licensinformation från LiveCycle ES.
* Fyll i `V2KeyParameters` objekt (som du hämtar genom att anropa `MediaEncrypter.getKeyParameters()`).
* Läs in `SigningCredential`, som är den paketeringsautentisering som utfärdas av Adobe och som används för att signera krypteringsmetadata. Skaffa `SignatureParameters` objekt genom anrop `MediaEncrypter.getSignatureParameters()` och fyll i signeringsuppgifter.
* Utlysning `MetaDataConverter.convertMetadata()` för att få `V2ContentMetaData`.
* Utlysning `V2ContentMetaData.getBytes()` och lagra för framtida bruk eller ringa `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
