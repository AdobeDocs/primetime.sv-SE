---
title: Primetime DRM-licensserver
description: Primetime DRM-licensserver
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Primetime DRM-licensserver {#primetime-drm-license-server}

Primetimes DRM-licensserver byggs från Primetimes DRM Java SDK. Den här servern förbrukar licensbegäranden från klienter som begär åtkomst till skyddat innehåll. Servern kan tolka och ändra DRM-principen inifrån licensbegäran för att ändra eller åsidosätta principen innan principen används för att generera en licens för den begärande klienten.

För att kunna distribuera en Primetime DRM-licensserver måste den först uppfylla **Adobe-kompatibilitetsreglerna och Robustness-reglerna** för Primetime DRM. Adobe erbjuder också en licensieringstjänst för Primetime DRM med namnet [Primetime Cloud DRM](../cloud-quick-start/whats-included.md) som du kan använda som ett alternativ till att använda din egen licensserver.
