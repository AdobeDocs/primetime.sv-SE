---
title: Översikt
description: Översikt
copied-description: true
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Översikt{#overview}

Om du vill begära en licens skickar klienten de metadata som var inbäddade i innehållet under paketeringen. Licensservern använder informationen i innehållets metadata för att generera en licens.

The `LicenseHandler` läser en licensbegäran och tolkar begäran. `LicenseHandler`extends `BatchHandlerBase` för att hantera grupplicensbegäranden, även om den här funktionen inte stöds av Adobe Access-klienter. The `getRequests()` metoden returnerar List of `LicenseRequestMessage` objekt. Anroparen bör iterera genom `LicenseRequestMessages`och för varje begäran antingen generera en licens eller ange en felkod (se `LicenseRequestMessage` API-referensdokumentation för mer information). För varje licensbegäran avgör servern om den kommer att utfärda en licens. Utlysning `LicenseRequestMessage.getContentInfo()` för att få information som extraherats från innehållets metadata, inklusive innehålls-ID, licens-ID och profiler.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot;/flashaccess/license/v4&quot;. Om protokollversion 3 är den högsta som stöds av antingen klienten eller servern skickar Adobe Access-klienterna autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot;/flashaccess/license/v3&quot;. Annars skickas autentiseringsbegäranden till&quot;License Server URL in metadata&quot; + &quot;/flashaccess/license/v1&quot;

Om ett fel inträffar när begäran analyseras, visas ett `HandlerParsingException` kastas. Undantaget innehåller felinformation som ska returneras till klienten. Om du vill hämta felinformationen ringer du `HandlerParsingException.getErrorData()`. Om ett fel inträffar när en licens genereras eftersom policykraven inte har uppfyllts, visas ett `PolicyEvaluationException` kastas. Undantaget innehåller även `ErrorData` som ska returneras till klienten. I API-dokumentationen finns mer information om `LicenseRequestMessage.generateLicense()` om du vill ha information om hur policyer utvärderas under generering av licenser.

Licenser och fel skickas samtidigt när `LicenseHandler.close()` anropas.

En enhet kan ha flera licenser för samma innehåll (samma licens-ID), men kan bara ha en licens för ett visst licens-ID och princip-ID. Om den får en licens med ett duplicerat LicenseID/PolicyID ersätter den nya licensen bara den gamla om den nya licensens utfärdandedatum infaller senare än den befintliga licensens utfärdandedatum. Den här logiken används för att bearbeta licenser som är inbäddade i innehållet, och du bör därför inte bädda in mer än en licens med samma princip-ID i ett innehållssegment. Samma logik gäller för licenser som skickas till klienten via `DRMManager.storeVoucher()` ActionScript3 API; Om klienten redan har en licens med ett senare utfärdandedatum kan den angivna licensen ignoreras.
