---
seo-title: Förgenererande licenser
title: Förgenererande licenser
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Förgenererande licenser{#pre-generating-licenses}

Om du vill generera licenser i förväg använder du `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` för att hämta en instans av `LicenseFactory`. En autentiseringsuppgift för licensservern måste anges för att de licenser som skapas av den här fabriken ska kunna signeras. Den här klassen har stöd för generering av Leaf-licenser utan licenssammanlänkning samt Leaf- och Root-licenser med den [förbättrade licenskolänkningen](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

När en Leaf-licens genereras måste innehållets metadata anges med `initContentInfo()`. Om metadata innehåller flera profiler, eller om du vill använda en profil som inte fanns i metadata, använder du `setSelectedPolicy()` för att ange vilken profil som ska användas för att generera licensen. Om du använder en principuppdateringslista för att spåra uppdateringar av profiler, kan du tillhandahålla principuppdateringslistan till License Factory innan du initierar metadata med `setPolicyUpdateList()`.

När du genererar en rotlicens kan innehållets metadata anges enligt beskrivningen ovan. En rotlicens kan också genereras med en princip ( `setSelectedPolicy()`) och en licensserver-URL ( `setLicenseServerURL()`) i stället för med metadata.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>En licensserver-URL krävs även om det inte finns någon Adobe Access-licensserver från vilken klienterna kan begära en licens. I det här fallet ska licensserverns URL ange en URL som identifierar licensutfärdaren.

Om principen använder Förbättrad licenskodning måste en autentiseringsuppgift för licensservern anges för att dekryptera rotkrypteringsnyckeln i principen ( `setRootKeyRetrievalInfo()`).

Om principen kräver en domänbunden licens använder du `setDomainCAs()` för att ange de domänutfärdare som licensservern ska acceptera domäntoken från. Ett eller flera certifikat för domän-certifikatutfärdare måste anges för att validera licensmottagaren.

Om principen kräver fjärrnyckelleverans för iOS-enheter måste nyckelservercertifikatet anges med `setKeyServerCertificate()`, såvida inte ett kedjat löv genereras.

Om du vill generera en licens anropar du `generateLicense()` och anger licenstypen (Leaf eller Root) och ett eller flera mottagarcertifikat. Mottagarcertifikatet är antingen ett datorcertifikat eller ett domäncertifikat, beroende på vilka krav som anges i profilen. Om du genererar ett kedjat löv krävs ingen mottagare. När licensen har skapats går det att åsidosätta användningsreglerna som har angetts i profilen. Anropa slutligen `signLicense()` för att signera licensen och få en instans av `PreGeneratedLicense`. Licensen kan nu sparas i en fil (använd `getBytes()` för att hämta den serialiserade licensen) eller bäddas in i krypterat innehåll. Se [Bädda in licenser](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Exempelkod som visar förgenererade licenser finns `com.adobe.flashaccess.samples.licensegen.GenerateLicense` i katalogen&quot;samples&quot; (Exempel) i kommandoradsverktygen för referensimplementering.
