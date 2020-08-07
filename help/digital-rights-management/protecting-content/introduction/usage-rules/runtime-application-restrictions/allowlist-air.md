---
description: 'null'
seo-description: 'null'
seo-title: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
title: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Ett tillåtelselista anger vilka AIR-, iOS- och Android-program som får spela upp innehåll. Det anger även program-ID:n för AIR och iOS, minimiversion, maxversion och utgivar-ID.

Exempel: Använd den här regeln om du vill begränsa uppspelningen till ett visst program eller om du vill styra vilken version av programmet som har åtkomst till innehållet.

>[!NOTE]
>
>Om du använder Adobe Flash Builder för att skapa skyddade program måste du se till att du inte distribuerar programmet i felsökningsläge. När du distribuerar ett program i felsökningsläge läggs Flash Builder `.debug` till i AIR-program-ID:t, vilket gör att tillåtelselista-funktionen i Primetime DRM beter sig oväntat.
