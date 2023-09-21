---
title: Felhantering av licensbegäran
description: Felhantering av licensbegäran
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Felhantering av licensbegäran {#license-request-error-handling}

Om ett fel inträffar under tolkningen av begäran, visas ett `HandlerParsingException` inträffar. Undantaget innehåller felinformation som returneras till klienten. Om du behöver hämta felinformationen måste du ringa `HandlerParsingException.getErrorData()`. Om ett fel inträffar under genereringen av en licens på grund av DRM-principkrav som inte har uppfyllts, kan en `PolicyEvaluationException` inträffar. Undantaget innehåller även `ErrorData` som ska returneras till klienten.

API-dokumentationen innehåller mer information om `LicenseRequestMessage.generateLicense()` om du vill ha mer information om hur DRM-principer utvärderas under licensgenerering.
