---
title: Hantera autentiseringsbegäranden
description: Hantera autentiseringsbegäranden
copied-description: true
exl-id: 64d23db0-254d-46b1-8317-ba0381509b44
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Hantera autentiseringsbegäranden {#handle-authentication-requests}

The `AuthenticationHandler` -klassen används för att bearbeta autentiseringsbegäranden. Den används endast för autentisering av användarnamn/lösenord.

När autentiseringstoken genereras måste tokens utgångsdatum anges. Anpassade egenskaper kan också inkluderas i token. Om detta anges visas dessa egenskaper för servern när autentiseringstoken skickas i efterföljande begäranden. Se [Hantera licensbegäranden](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) om du vill ha information om hur du hanterar anpassade autentiseringstoken.

Hanteraren läser en autentiseringsbegäran och tolkar begärandemeddelandet när `parseRequest()` anropas. Serverimplementeringen undersöker användarautentiseringsuppgifterna i begäran och om autentiseringsuppgifterna är giltiga genererar en `AuthenticationToken` objekt genom anrop `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` anropas inte före `close()`, skickas en felkod för autentiseringsfel.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Om protokollversion 3 är den maximala som stöds av antingen klienten eller servern skickar Adobe Primetime DRM-klienter autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. Annars skickas autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;
