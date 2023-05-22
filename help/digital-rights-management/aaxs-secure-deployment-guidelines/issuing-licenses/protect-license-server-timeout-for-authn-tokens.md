---
title: Timeout för autentiseringstoken
description: Timeout för autentiseringstoken
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Access SDK har ett tidsgränsintervall för att skydda programsäkerheten. Giltigheten för autentiseringstoken anges med Adobe Access SDK när en autentiseringsbegäran hanteras. När förfallotiden har passerat är autentiseringstoken inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i AuthenticationHandler i *API-referens för Adobe Access*.
