---
title: Felhantering av licensbegäran
description: Felhantering av licensbegäran
copied-description: true
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Felhantering av licensbegäran {#license-request-error-handling}

Om ett fel inträffar under tolkningen av begäran, visas ett `HandlerParsingException` inträffar. Undantaget innehåller felinformation som returneras till klienten. Om du behöver hämta felinformationen måste du ringa `HandlerParsingException.getErrorData()`. Om ett fel inträffar under genereringen av en licens på grund av DRM-principkrav som inte har uppfyllts, kan en `PolicyEvaluationException` inträffar. Undantaget innehåller även `ErrorData` som ska returneras till klienten.

I API-dokumentationen finns mer information om `LicenseRequestMessage.generateLicense()` om du vill ha mer information om hur DRM-principer utvärderas under licensgenerering.
