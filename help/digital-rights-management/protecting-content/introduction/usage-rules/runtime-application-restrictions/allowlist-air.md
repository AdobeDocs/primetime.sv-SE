---
description: 'null'
seo-description: 'null'
seo-title: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
title: Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Tillåtelselista för Primetimes DRM-program tillåts spela upp skyddat innehåll {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Ett tillåtelselista anger vilka AIR-, iOS- och Android-program som får spela upp innehåll. Det anger även program-ID:n för AIR och iOS, minimiversion, maxversion och utgivar-ID.

Exempel: Använd den här regeln om du vill begränsa uppspelningen till ett visst program eller om du vill styra vilken version av programmet som har åtkomst till innehållet.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om du använder Adobe Flash Builder för att skapa skyddade program måste du se till att du inte distribuerar programmet i felsökningsläge. När du distribuerar ett program i felsökningsläge läggs Flash Builder `.debug` till i AIR-program-ID:t, vilket gör att tillåtelselista-funktionen i Primetime DRM fungerar oväntat.
