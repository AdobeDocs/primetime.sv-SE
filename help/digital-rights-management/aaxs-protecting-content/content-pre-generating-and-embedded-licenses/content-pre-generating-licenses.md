---
title: Förgenererande licenser
description: Förgenererande licenser
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Förgenererande licenser{#pre-generating-licenses}

Om du vill förgenerera licenser använder du `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` för att hämta en instans av `LicenseFactory`. En autentiseringsuppgift för licensservern måste anges för att de licenser som genereras av den här fabriken ska kunna signeras. Den här klassen har stöd för generering av Leaf-licenser utan licenskedning samt Leaf- och Root-licenser med [Förbättrad kedja av licenser](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

När en Leaf-licens genereras måste innehållets metadata anges med `initContentInfo()`. Om metadata innehåller flera principer, eller om du vill använda en profil som inte fanns i metadata, använder du `setSelectedPolicy()` för att ange vilken profil som ska användas för att generera licensen. Om du använder en principuppdateringslista för att spåra uppdateringar av profiler kan du tillhandahålla principuppdateringslistan till licensfabriken innan du initierar metadata med `setPolicyUpdateList()`.

När du genererar en rotlicens kan innehållets metadata anges enligt beskrivningen ovan. Du kan även skapa en rotlicens med hjälp av en princip ( `setSelectedPolicy()`) och licensserverns URL ( `setLicenseServerURL()`) istället för metadata.

>[!NOTE]
>
>En licensserver-URL krävs även om det inte finns någon Adobe Access-licensserver från vilken klienterna kan begära en licens. I det här fallet ska licensserverns URL ange en URL som identifierar licensutfärdaren.

Om principen använder Förbättrad licenskolkning måste en autentiseringsuppgift för licensservern anges för att dekrypteringsnyckeln för roten ska kunna dekrypteras i principen ( `setRootKeyRetrievalInfo()`).

Om principen kräver en domänbunden licens kan du använda `setDomainCAs()` för att ange de domänutfärdare som licensservern ska acceptera domäntoken från. Ett eller flera certifikat för domän-certifikatutfärdare måste anges för att validera licensmottagaren.

Om principen kräver fjärrnyckelleverans för iOS-enheter måste nyckelservercertifikatet anges med `setKeyServerCertificate()`, såvida inte ett kedjat löv genereras.

Om du vill generera en licens anropar du `generateLicense()` och ange licenstypen (Leaf eller Root) och ett eller flera mottagarcertifikat. Mottagarcertifikatet är antingen ett datorcertifikat eller ett domäncertifikat, beroende på vilka krav som anges i profilen. Om du genererar ett kedjat löv krävs ingen mottagare. När licensen har skapats går det att åsidosätta användningsreglerna som har angetts i profilen. Äntligen, anropa `signLicense()` för att signera licensen och få en instans av `PreGeneratedLicense`. Licensen kan nu sparas i en fil (använd `getBytes()` för att hämta den serialiserade licensen) eller inbäddat i krypterat innehåll. Se, [Bädda in licenser](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Exempelkod som visar förgenererade licenser finns i `com.adobe.flashaccess.samples.licensegen.GenerateLicense` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
