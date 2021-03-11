---
description: Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.
title: Timeout för autentiseringstoken
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.

Giltigheten för autentiseringstoken anges med hjälp av DRM SDK-inställningen Primetime när en autentiseringsförfrågan hanteras. När den har gått ut är token inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
