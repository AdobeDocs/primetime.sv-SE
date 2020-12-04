---
description: Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.
seo-description: Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.
seo-title: Timeout för autentiseringstoken
title: Timeout för autentiseringstoken
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.

Giltigheten för autentiseringstoken anges med hjälp av DRM SDK-inställningen Primetime när en autentiseringsförfrågan hanteras. När den har gått ut är token inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
