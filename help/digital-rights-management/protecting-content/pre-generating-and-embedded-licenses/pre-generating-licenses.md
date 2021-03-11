---
description: Om du använder Adobe Primetime DRM Professional kan du generera licenser i förväg och bädda in licenser i innehållet. Den här funktionen kan kombineras med förbättrad licenskedning, så att en lövlicens är förgenererad och inbäddad i innehållet, och klienten kan begära en rotlicens (bunden till en dator eller domän) från en licensserver. Alternativt kan klientprogram implementera ett arbetsflöde där enheten förregistrerar sig hos en server, servern förgenererar licenser som är bundna till den enheten och klienten hämtar sina licenser från en enkel HTTP-webbserver.
title: Förgenererande licenser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Förgenererande licenser {#pre-generating-licenses}

Om du använder Adobe Primetime DRM Professional kan du generera licenser i förväg och bädda in licenser i innehållet. Den här funktionen kan kombineras med förbättrad licenskedning, så att en lövlicens är förgenererad och inbäddad i innehållet, och klienten kan begära en rotlicens (bunden till en dator eller domän) från en licensserver. Alternativt kan klientprogram implementera ett arbetsflöde där enheten förregistrerar sig hos en server, servern förgenererar licenser som är bundna till den enheten och klienten hämtar sina licenser från en enkel HTTP-webbserver.

Om du vill förgenerera licenser måste du använda `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` för att hämta en instans av `LicenseFactory`. Du måste ange en autentiseringsuppgift för licensservern för att signera de licenser som genereras av den här fabriken. Den här klassen har stöd för generering av Leaf-licenser utan licenskedning samt Leaf- och Root-licenser med [Förbättrad licenskedning](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

När du genererar en Leaf-licens måste du ange innehållets metadata som gäller `initContentInfo()`. Om metadata innehåller flera DRM-principer, eller om du vill använda en DRM-princip som inte ingår i metadata, måste du använda `setSelectedPolicy()` för att ange DRM-principen för att generera en licens. Om du använder en DRM-principuppdateringslista för att spåra uppdateringar av DRM-principer kan du tillhandahålla DRM-principuppdateringslistan till licensfabriken innan du initierar metadata med `setPolicyUpdateList()`.

När du genererar en rotlicens måste du ange innehållets metadata enligt beskrivningen ovan. Du kan också generera en rotlicens genom att tillämpa en DRM-princip ( `setSelectedPolicy()`) och en licensserver-URL ( `setLicenseServerURL()`) i stället för metadata.

>[!NOTE]
>
>En licensserver-URL krävs även om det inte finns någon Adobe Primetime DRM-licensserver från vilken klienterna kan begära en licens. I det här fallet ska licensserverns URL ange en URL som identifierar licensutfärdaren.

Om DRM-principen använder Förbättrad licenskodning måste du ange en autentiseringsuppgift för licensservern för att dekryptera rotkrypteringsnyckeln i DRM-principen ( `setRootKeyRetrievalInfo()`).

Om DRM-principen kräver en domänbunden licens måste du använda `setDomainCAs()` för att ange de domänutfärdare som licensservern accepterar domäntoken från. Ett eller flera certifikat för domän-certifikatutfärdare måste anges för att validera licensmottagaren.

Om DRM-principen kräver fjärrnyckelleverans för iOS-enheter måste du ange nyckelservercertifikatet genom att använda `setKeyServerCertificate()` om inte ett kedjat löv genereras.

Om du vill generera en licens måste du anropa `generateLicense()` och ange licenstypen (Leaf eller Root) samt ett eller flera mottagarcertifikat. Mottagarcertifikatet representerar antingen ett datorcertifikat eller ett domäncertifikat, beroende på vilka krav som anges i DRM-principen. Om du genererar ett kedjat löv krävs ingen mottagare. När licensen har skapats kan du åsidosätta användningsreglerna som har angetts i DRM-principen. Slutligen måste du anropa `signLicense()` för att signera licensen och få en instans av `PreGeneratedLicense`. Licensen kan nu sparas (använd `getBytes()` för att hämta den serialiserade licensen eller bädda in i krypterat innehåll.

Se [Bädda in licenser](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Se `com.adobe.flashaccess.samples.licensegen.GenerateLicense` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot; för exempelkod om hur du demonstrerar förgenererade licenser.
