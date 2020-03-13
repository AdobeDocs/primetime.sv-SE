---
seo-title: Hantera autentiseringsbegäranden
title: Hantera autentiseringsbegäranden
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Hantera autentiseringsbegäranden {#handle-authentication-requests}

Klassen används `AuthenticationHandler` för att bearbeta autentiseringsbegäranden. Den används endast för autentisering av användarnamn/lösenord.

När autentiseringstoken genereras måste tokens utgångsdatum anges. Anpassade egenskaper kan också inkluderas i token. Om detta anges visas dessa egenskaper för servern när autentiseringstoken skickas i efterföljande begäranden. Mer information om hur du hanterar anpassade autentiseringstoken finns i [Hantera licensbegäranden](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) .

Hanteraren läser en autentiseringsbegäran och tolkar begärandemeddelandet när `parseRequest()` anropas. Serverimplementeringen undersöker inloggningsuppgifterna i begäran och om inloggningsuppgifterna är giltiga genererar ett `AuthenticationToken` objekt genom att anropa `getRequest().generateAuthToken()`. Om `AuthenticationRequestMessage.generateAuthToken()` inte anropas tidigare `close()`skickas en felkod för autentiseringsfel.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Om protokollversion 3 är den högsta som stöds av antingen klienten eller servern skickar Adobe Primetime DRM-klienter autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. Annars skickas autentiseringsbegäranden till licensserverns URL i metadata + &quot; [!DNL /flashaccess/authn/v1]&quot;

