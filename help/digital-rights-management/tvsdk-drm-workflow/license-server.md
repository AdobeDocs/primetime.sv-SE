---
title: Primetime DRM-licensserver
description: Primetime DRM-licensserver
copied-description: true
exl-id: 2927bb21-0001-46d4-aae1-a277f414560d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Primetime DRM-licensserver {#primetime-drm-license-server}

Primetimes DRM-licensserver byggs från Primetimes DRM Java SDK. Den här servern förbrukar licensbegäranden från klienter som begär åtkomst till skyddat innehåll. Servern kan tolka och ändra DRM-principen inifrån licensbegäran för att ändra eller åsidosätta principen innan principen används för att generera en licens för den begärande klienten.

För att kunna distribuera en Primetime DRM-licensserver måste den uppfylla **Regler för efterlevnad och tillförlitlighet i Adobe** för Primetime DRM. Adobe erbjuder också en DRM-licensieringstjänst som heter Primetime [Primetime Cloud DRM](../cloud-quick-start/whats-included.md), som du kan använda som ett alternativ till att vara värd för din egen licensserver.
