---
seo-title: Timeout för autentiseringstoken
title: Timeout för autentiseringstoken
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Access SDK har ett tidsgränsintervall för att skydda programsäkerheten. Giltigheten för autentiseringstoken anges med Adobe Access SDK när en autentiseringsbegäran hanteras. När förfallotiden har passerat är autentiseringstoken inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i AuthenticationHandler i *API-referens för Adobe Access*.
