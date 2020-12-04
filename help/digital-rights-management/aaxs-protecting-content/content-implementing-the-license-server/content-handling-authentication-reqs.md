---
seo-title: Hantera autentiseringsbegäranden
title: Hantera autentiseringsbegäranden
uuid: 036582d4-611c-4772-b247-81a3144fd5d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Hantera autentiseringsbegäranden{#handling-authentication-requests}

Klassen `AuthenticationHandler` används för att bearbeta autentiseringsbegäranden. Den används endast för autentisering av användarnamn/lösenord.

När autentiseringstoken genereras måste tokens utgångsdatum anges. Anpassade egenskaper kan också inkluderas i token. Om detta anges visas dessa egenskaper för servern när autentiseringstoken skickas i efterföljande begäranden. Mer information om hur du hanterar anpassade autentiseringstoken finns i [Hantera licensbegäranden](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md).

Hanteraren läser en autentiseringsbegäran och tolkar begärandemeddelandet när `parseRequest()` anropas. Serverimplementeringen undersöker inloggningsuppgifterna i begäran och om inloggningsuppgifterna är giltiga genererar ett `AuthenticationToken`-objekt genom att anropa `getRequest().generateAuthToken()`. Om `AuthenticationRequestMessage.generateAuthToken()` inte anropas före `close()` skickas en felkod för autentiseringsfel.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot;/flashaccess/authn/v4&quot;. Om protokollversion 3 är den högsta som stöds av antingen klienten eller servern skickar Adobe Access-klienterna autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot;/flashaccess/authn/v3&quot;. Annars skickas autentiseringsbegäranden till licensserverns URL i metadata + /flashaccess/authn/v1

