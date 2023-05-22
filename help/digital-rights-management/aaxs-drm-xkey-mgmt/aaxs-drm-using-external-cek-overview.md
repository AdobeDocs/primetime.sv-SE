---
description: Kunder kan använda Adobe Access (AAXS) DRM med sina egna CMS-system (Content Key Management System) med funktionen External CEK.
title: Extern CEK-översikt för Adobe Access DRM
exl-id: 4131863b-5773-4222-aae9-d984267cdb86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Extern CEK-översikt för Adobe Access DRM {#adobe-access-drm-external-cek-overview}

Kunder kan använda Adobe Access (AAXS) DRM med sina egna CMS-system (Content Key Management System) med funktionen External CEK.

Adobe Access (AAXS) DRM abstraherar som standard behovet av att hantera nycklar, certifikat och DRM-metadata direkt under innehållspaketeringsprocessen. AAXS Java SDK genererar automatiskt en slumpmässig innehållskrypteringsnyckel (CEK) under paketeringstiden och använder den för att kryptera innehållet. Därefter krypterar SDK själva CEK:n och infogar den i innehållets metadata. Vid utfärdandet av licenser behöver AXS-servern bara den privata nyckeln för AAXS-licensservern för att få åtkomst till CEK från metadata för att generera en licens.
