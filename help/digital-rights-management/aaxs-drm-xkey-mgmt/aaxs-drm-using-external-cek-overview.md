---
description: Kunder kan använda Adobe Access (AAXS) DRM med sina egna CMS-system (Content Key Management System) med funktionen External CEK.
seo-description: Kunder kan använda Adobe Access (AAXS) DRM med sina egna CMS-system (Content Key Management System) med funktionen External CEK.
seo-title: Extern CEK-översikt för Adobe Access DRM
title: Extern CEK-översikt för Adobe Access DRM
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Extern CEK-översikt för Adobe Access DRM {#adobe-access-drm-external-cek-overview}

Kunder kan använda Adobe Access (AAXS) DRM med sina egna CMS-system (Content Key Management System) med funktionen External CEK.

Adobe Access (AAXS) DRM abstraherar som standard behovet av att hantera nycklar, certifikat och DRM-metadata direkt under innehållspaketeringsprocessen. AAXS Java SDK genererar automatiskt en slumpmässig innehållskrypteringsnyckel (CEK) under paketeringstiden och använder den för att kryptera innehållet. Därefter krypterar SDK själva CEK:n och infogar den i innehållets metadata. Vid utfärdandet av licenser behöver AXS-servern bara den privata nyckeln för AAXS-licensservern för att få åtkomst till CEK från metadata för att generera en licens.
