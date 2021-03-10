---
title: Hantera domänregistreringsbegäranden
description: Hantera domänregistreringsbegäranden
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Hantera domänregistreringsbegäranden{#handling-domain-registration-requests}

Om DRM-metadata indikerar att en domänregistrering behövs för att spela upp innehållet, ska klientprogrammet anropa ActionScript-API:t för DRMManager.addToDeviceGroup() eller joinLicenseDomain() för iOS. Om klienten ännu inte har registrerat sig på den angivna domänservern (eller om programmet tvingar fram ett nytt medlemskap) skickas en begäran om domänregistrering. Domänservern avgör om klienten har behörighet att ansluta till en domän och utfärdar en eller flera domänautentiseringsuppgifter till klienten.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;Domänserver-URL i metadata: + &quot;/flashaccess/domain/v4&quot;. I annat fall är begärande-URL:en Domänserverns URL i metadata&quot; + &quot;/flashaccess/domain/v3&quot;

När du initierar `DomainRegistrationHandler` måste domänserverns URL anges. Den här URL:en inkluderas i de domäntoken som utfärdas av hanteraren för att ange domänservern som utfärdade token. URL:en måste matcha domänserverns URL som anges i en princip som kräver domänregistrering med servern.

För att avgöra om klienten har behörighet att ansluta till domänen kan servern undersöka dator- och användarinformationen i begäran. Mer information om hur du identifierar och räknar datorer som ansluter till domänen finns i [Använda datoridentifierare](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md). Servern kan också avgöra vilken domän klienten har behörighet att ansluta till. Observera att en klient bara kan vara medlem i en domän per domänserver-URL. Om datorn redan har en domäntoken för den här domänserverns URL kommer domänregistreringsbegäran att inkludera det aktuella domännamnet ( `getRequestDomainName()`). För en begäran om återanslutning måste domänservern antingen returnera den aktuella uppsättningen domänreferenser för den här domänen eller returnera ett fel (domänservern kanske inte returnerar domänens autentiseringsuppgifter för en annan domän).

Om domänservern kräver autentisering för att ansluta till en domän bör begäran innehålla en autentiseringstoken. Precis som med en licensbegäran kan domänregistrering kräva användarnamn/lösenord eller anpassad autentisering. Mer information om hur du hanterar autentiseringstoken finns i [Användarautentisering](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md).

Domänservern ansvarar för att lagra och hantera de domännycklar som är associerade med varje domän. När ett nytt nyckelpar måste skapas för en domän (domänens första domänregistrering), anropar du `generateDomainCredential` `(String, int, Principal, Date)`. Den här metoden genererar ett nytt domännyckelpar och domäncertifikat. Domänservern måste lagra den privata nyckeln och certifikatet och tillhandahålla dessa objekt när efterföljande begäranden för den här domänen behandlas. Det går också att generera ett nytt nyckelpar för en domän för att kunna föra över nycklarna. När du för pekaren över nycklarna för en viss domän måste du även öka nyckelversionen i `generateDomainCredential`.

Varje gång en dator registrerar sig med samma domän bör samma privata nyckel och certifikat för domänen användas. Anropa `addDomainCredential(DomainToken, PrivateKey)` om du vill returnera en befintlig domänreferens till klienten. Om det finns flera domänautentiseringsuppgifter för domänen eftersom domännycklarna har ändrats, bör servern ange domänautentiseringsuppgifter för den aktuella domännyckeln och alla tidigare domännycklar så att klienten kan förbruka licenser bundna till äldre domännycklar. Detta gör att en licens som är bunden till en gammal domäntoken kan flyttas till en nyligen registrerad dator och fortfarande kan spelas upp.
