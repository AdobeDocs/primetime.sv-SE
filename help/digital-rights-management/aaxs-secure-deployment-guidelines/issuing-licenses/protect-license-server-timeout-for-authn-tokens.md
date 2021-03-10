---
title: Timeout för autentiseringstoken
description: Timeout för autentiseringstoken
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Access SDK har ett tidsgränsintervall för att skydda programsäkerheten. Giltigheten för autentiseringstoken anges med Adobe Access SDK när en autentiseringsbegäran hanteras. När förfallotiden har passerat är autentiseringstoken inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i AuthenticationHandler i *API-referens för Adobe Access*.
