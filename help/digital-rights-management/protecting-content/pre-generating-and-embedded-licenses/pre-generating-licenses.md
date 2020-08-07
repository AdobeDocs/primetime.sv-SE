---
description: Om du använder Adobe Primetime DRM Professional kan du generera licenser i förväg och bädda in licenser i innehållet. Den här funktionen kan kombineras med förbättrad licenskedning, så att en lövlicens är förgenererad och inbäddad i innehållet, och klienten kan begära en rotlicens (bunden till en dator eller domän) från en licensserver. Alternativt kan klientprogram implementera ett arbetsflöde där enheten förregistrerar sig hos en server, servern förgenererar licenser som är bundna till den enheten och klienten hämtar sina licenser från en enkel HTTP-webbserver.
seo-description: Om du använder Adobe Primetime DRM Professional kan du generera licenser i förväg och bädda in licenser i innehållet. Den här funktionen kan kombineras med förbättrad licenskedning, så att en lövlicens är förgenererad och inbäddad i innehållet, och klienten kan begära en rotlicens (bunden till en dator eller domän) från en licensserver. Alternativt kan klientprogram implementera ett arbetsflöde där enheten förregistrerar sig hos en server, servern förgenererar licenser som är bundna till den enheten och klienten hämtar sina licenser från en enkel HTTP-webbserver.
seo-title: Förgenererande licenser
title: Förgenererande licenser
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# Förgenererande licenser {#pre-generating-licenses}

Om du använder Adobe Primetime DRM Professional kan du generera licenser i förväg och bädda in licenser i innehållet. Den här funktionen kan kombineras med förbättrad licenskedning, så att en lövlicens är förgenererad och inbäddad i innehållet, och klienten kan begära en rotlicens (bunden till en dator eller domän) från en licensserver. Alternativt kan klientprogram implementera ett arbetsflöde där enheten förregistrerar sig hos en server, servern förgenererar licenser som är bundna till den enheten och klienten hämtar sina licenser från en enkel HTTP-webbserver.

Om du vill förgenerera licenser måste du använda `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` för att hämta en instans av `LicenseFactory`. Du måste ange en autentiseringsuppgift för licensservern för att signera de licenser som genereras av den här fabriken. Den här klassen har stöd för generering av Leaf-licenser utan licenssammanlänkning samt Leaf- och Root-licenser med den [förbättrade licenskolänkningen](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

När du genererar en Leaf-licens måste du ange de innehålls-metadata som gäller `initContentInfo()`. Om metadata innehåller flera DRM-principer, eller om du vill använda en DRM-princip som inte ingår i metadata, måste du använda `setSelectedPolicy()` för att ange DRM-principen för att generera en licens. Om du använder en DRM-principuppdateringslista för att spåra uppdateringar av DRM-principer, kan du tillhandahålla DRM-principuppdateringslistan till License Factory innan du initierar metadata med `setPolicyUpdateList()`.

När du genererar en rotlicens måste du ange innehållets metadata enligt beskrivningen ovan. Du kan också generera en rotlicens genom att tillämpa en DRM-princip ( `setSelectedPolicy()`) och en licensserver-URL ( `setLicenseServerURL()`) i stället för metadata.

>[!NOTE]
>
>En licensserver-URL krävs även om det inte finns någon Adobe Primetime DRM-licensserver från vilken klienterna kan begära en licens. I det här fallet ska licensserverns URL ange en URL som identifierar licensutfärdaren.

Om DRM-principen använder Förbättrad licenskodning måste du ange en autentiseringsuppgift för licensservern för att dekryptera rotkrypteringsnyckeln i DRM-principen ( `setRootKeyRetrievalInfo()`).

Om DRM-principen kräver en domänbunden licens måste du använda `setDomainCAs()` för att ange de domänutfärdare som licensservern accepterar domäntoken från. Ett eller flera certifikat för domän-certifikatutfärdare måste anges för att validera licensmottagaren.

Om DRM-principen kräver fjärrnyckelleverans för iOS-enheter måste du ange nyckelservercertifikatet genom att tillämpa `setKeyServerCertificate()` såvida inte ett kedjat löv genereras.

Om du vill generera en licens måste du anropa `generateLicense()` och ange licenstypen (Leaf eller Root) och ett eller flera mottagarcertifikat. Mottagarcertifikatet representerar antingen ett datorcertifikat eller ett domäncertifikat, beroende på vilka krav som anges i DRM-principen. Om du genererar ett kedjat löv krävs ingen mottagare. När licensen har skapats kan du åsidosätta användningsreglerna som har angetts i DRM-principen. Slutligen måste du anropa `signLicense()` för att signera licensen och få en instans av `PreGeneratedLicense`. Licensen kan nu sparas (används `getBytes()` för att hämta den serialiserade licensen eller bäddas in i krypterat innehåll.

Se [Bädda in licenser](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

I katalogen&quot;samples&quot; (Exempel) `com.adobe.flashaccess.samples.licensegen.GenerateLicense` för kommandoradsverktygen för referensimplementering finns exempelkod om hur du demonstrerar förgenererade licenser.
