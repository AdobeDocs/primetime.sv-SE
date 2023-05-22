---
title: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
description: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
copied-description: true
exl-id: c5aced0f-2c38-4ae7-9a33-44877e57a993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

A tillåtelselista anger vilka AIR-, iOS- och Android-program som får spela upp innehåll. Det anger även program-ID:n för AIR och iOS, minimiversion, maxversion och utgivar-ID.

Exempel: Använd den här regeln om du vill begränsa uppspelningen till ett visst program eller om du vill styra vilken version av programmet som har åtkomst till innehållet.

>[!NOTE]
>
>Om du använder Adobe Flash Builder för att skapa skyddade program måste du se till att du inte distribuerar programmet i felsökningsläge. När du distribuerar ett program i felsökningsläge läggs Flash Builder till `.debug` till AIR program-ID, som sedan får tillåtelselista-funktionen i Primetime DRM att uppträda oväntat.
