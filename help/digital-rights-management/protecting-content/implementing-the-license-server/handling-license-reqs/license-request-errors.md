---
seo-title: Felhantering av licensbegäran
title: Felhantering av licensbegäran
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Felhantering av licensbegäran {#license-request-error-handling}

Om ett fel inträffar under tolkningen av begäran inträffar en `HandlerParsingException`. Undantaget innehåller felinformation som returneras till klienten. Om du behöver hämta felinformationen måste du ringa `HandlerParsingException.getErrorData()`. Om ett fel inträffar under genereringen av en licens på grund av DRM-principkrav som inte har uppfyllts, inträffar en `PolicyEvaluationException`. Det här undantaget innehåller även `ErrorData` som ska returneras till klienten.

Se API-dokumentationen för `LicenseRequestMessage.generateLicense()` för mer information om hur DRM-principer utvärderas under licensgenerering.
