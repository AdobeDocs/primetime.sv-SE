---
title: Hantera domänregistreringsbegäranden
description: Hantera domänregistreringsbegäranden
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Hantera domänregistreringsbegäranden{#handling-domain-registration-requests}

Om DRM-metadata anger att en domänregistrering behövs för att spela upp innehållet, ska klientprogrammet anropa ActionScriptet API:t DRMManager.addToDeviceGroup() eller joinLicenseDomain() i iOS. Om klienten ännu inte har registrerat sig på den angivna domänservern (eller om programmet tvingar fram ett nytt medlemskap) skickas en begäran om domänregistrering. Domänservern avgör om klienten har behörighet att ansluta till en domän och utfärdar en eller flera domänautentiseringsuppgifter till klienten.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Om både klienten och servern stöder protokoll version 5 är begäran-URL:en &quot;Domänserver-URL i metadata: + &quot;/flashaccess/domain/v4&quot;. I annat fall är begärande-URL:en Domänserverns URL i metadata&quot; + &quot;/flashaccess/domain/v3&quot;

Vid initiering av `DomainRegistrationHandler`måste domänserverns URL anges. Den här URL:en inkluderas i de domäntoken som utfärdas av hanteraren för att ange domänservern som utfärdade token. URL:en måste matcha domänserverns URL som anges i en princip som kräver domänregistrering med servern.

För att avgöra om klienten har behörighet att ansluta till domänen kan servern undersöka dator- och användarinformationen i begäran. Se [Använda datoridentifierare](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) om du vill ha information om hur du identifierar och räknar datorer som ansluter till domänen. Servern kan också avgöra vilken domän klienten har behörighet att ansluta till. Observera att en klient bara kan vara medlem i en domän per domänserver-URL. Om datorn redan har en domäntoken för den här domänserverns URL kommer domänregistreringsbegäran att inkludera det aktuella domännamnet ( `getRequestDomainName()`). För en begäran om återanslutning måste domänservern antingen returnera den aktuella uppsättningen domänreferenser för den här domänen eller returnera ett fel (domänservern kanske inte returnerar domänens autentiseringsuppgifter för en annan domän).

Om domänservern kräver autentisering för att ansluta till en domän bör begäran innehålla en autentiseringstoken. Precis som med en licensbegäran kan domänregistrering kräva användarnamn/lösenord eller anpassad autentisering. Se [Användarautentisering](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) om du vill ha information om hur du hanterar autentiseringstoken.

Domänservern ansvarar för att lagra och hantera de domännycklar som är associerade med varje domän. När ett nytt nyckelpar måste skapas för en domän (domänens första domänregistrering), anropar du `generateDomainCredential` `(String, int, Principal, Date)`. Den här metoden genererar ett nytt domännyckelpar och domäncertifikat. Domänservern måste lagra den privata nyckeln och certifikatet och tillhandahålla dessa objekt när efterföljande begäranden för den här domänen behandlas. Det går också att generera ett nytt nyckelpar för en domän för att kunna föra över nycklarna. När du håller tangenterna för en viss domän över måste du se till att öka nyckelversionen i `generateDomainCredential` också.

Varje gång en dator registrerar sig med samma domän bör samma privata nyckel och certifikat för domänen användas. Anropa `addDomainCredential(DomainToken, PrivateKey)` om du vill returnera en befintlig domänreferens till klienten. Om det finns flera domänautentiseringsuppgifter för domänen eftersom domännycklarna har ändrats, bör servern ange domänautentiseringsuppgifter för den aktuella domännyckeln och alla tidigare domännycklar så att klienten kan förbruka licenser som är bundna till äldre domännycklar. Detta gör att en licens som är bunden till en gammal domäntoken kan flyttas till en nyligen registrerad dator och fortfarande kan spelas upp.
