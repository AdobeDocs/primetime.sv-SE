---
title: Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll
description: Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll {#allowlist-for-adobe-primetime-applications-allowed-to-play-protected-content}

Anger vilka AIR-/iOS-program som kan spela upp innehåll. Ange program-ID för AIR/iOS, minimiversion, maxversion och utgivar-ID.

Exempel: Använd den här regeln om du vill begränsa uppspelningen till ett visst AIR/iOS-program eller om du vill styra vilken version som kan få åtkomst till innehållet.

>[!NOTE]
>
>Om du använder Adobe Flash Builder för att skapa skyddade program ska du se till att du inte distribuerar programmet i felsökningsläge. När du distribuerar ett program i felsökningsläge kommer Flash Builder att lägga till&quot;.debug&quot; i AIR-program-ID:t. Detta kommer att få tillåtelselista i Adobe Access att uppträda oväntat.

