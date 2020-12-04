---
seo-title: Översikt
title: Översikt
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Översikt{#overview}

Om du vill begära en licens skickar klienten de metadata som var inbäddade i innehållet under paketeringen. Licensservern använder informationen i innehållets metadata för att generera en licens.

`LicenseHandler` läser en licensbegäran och tolkar begäran. `LicenseHandler`utökas  `BatchHandlerBase` för att passa batchlicensbegäranden, även om den här funktionen inte stöds av Adobe Access-klienter. Metoden `getRequests()` returnerar en List med `LicenseRequestMessage`-objekt. Anroparen bör iterera genom `LicenseRequestMessages` och för varje begäran antingen generera en licens eller ange en felkod (mer information finns i API-referensdokumentationen för `LicenseRequestMessage`). För varje licensbegäran avgör servern om den kommer att utfärda en licens. Ring `LicenseRequestMessage.getContentInfo()` för att få information som extraherats från innehållets metadata, inklusive innehålls-ID, licens-ID och profiler.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot;/flashaccess/license/v4&quot;. Om protokollversion 3 är den högsta som stöds av antingen klienten eller servern skickar Adobe Access-klienterna autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot;/flashaccess/license/v3&quot;. Annars skickas autentiseringsbegäranden till&quot;License Server URL in metadata&quot; + &quot;/flashaccess/license/v1&quot;

Om ett fel inträffar när begäran tolkas genereras ett `HandlerParsingException`-fel. Undantaget innehåller felinformation som ska returneras till klienten. Om du vill hämta felinformationen ringer du `HandlerParsingException.getErrorData()`. Om ett fel inträffar när en licens genereras eftersom principkraven inte har uppfyllts, genereras ett `PolicyEvaluationException`-fel. Det här undantaget innehåller även `ErrorData` som ska returneras till klienten. Se API-dokumentationen för `LicenseRequestMessage.generateLicense()` för mer information om hur principer utvärderas under generering av licenser.

Licenser och fel skickas samtidigt när `LicenseHandler.close()` anropas.

En enhet kan ha flera licenser för samma innehåll (samma licens-ID), men kan bara ha en licens för ett visst licens-ID och princip-ID. Om den får en licens med ett duplicerat LicenseID/PolicyID ersätter den nya licensen bara den gamla om den nya licensens utfärdandedatum infaller senare än den befintliga licensens utfärdandedatum. Den här logiken används för att bearbeta licenser som är inbäddade i innehållet, och du bör därför inte bädda in mer än en licens med samma princip-ID i ett innehållssegment. Samma logik gäller för licenser som skickas till klienten via ActionScript3-API:t `DRMManager.storeVoucher()`. Om klienten redan har en licens med ett senare utfärdandedatum kan den angivna licensen ignoreras.
