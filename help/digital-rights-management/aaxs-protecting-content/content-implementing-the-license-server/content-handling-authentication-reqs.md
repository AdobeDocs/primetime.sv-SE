---
title: Hantera autentiseringsbegäranden
description: Hantera autentiseringsbegäranden
copied-description: true
exl-id: c1d46ec0-e053-4824-b3b1-20320e259fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Hantera autentiseringsbegäranden{#handling-authentication-requests}

The `AuthenticationHandler` -klassen används för att bearbeta autentiseringsbegäranden. Den används endast för autentisering av användarnamn/lösenord.

När autentiseringstoken genereras måste tokens utgångsdatum anges. Anpassade egenskaper kan också inkluderas i token. Om detta anges visas dessa egenskaper för servern när autentiseringstoken skickas i efterföljande begäranden. Se [Hantera licensbegäranden](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) om du vill ha information om hur du hanterar anpassade autentiseringstoken.

Hanteraren läser en autentiseringsbegäran och tolkar begärandemeddelandet när `parseRequest()` anropas. Serverimplementeringen undersöker användarautentiseringsuppgifterna i begäran och om autentiseringsuppgifterna är giltiga genererar en `AuthenticationToken` objekt genom anrop `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` anropas inte före `close()`, skickas en felkod för autentiseringsfel.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot;/flashaccess/authn/v4&quot;. Om protokollversion 3 är den högsta som stöds av antingen klienten eller servern skickar Adobe Access-klienterna autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot;/flashaccess/authn/v3&quot;. Annars skickas autentiseringsbegäranden till licensserverns URL i metadata + /flashaccess/authn/v1
