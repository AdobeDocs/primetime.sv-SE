---
title: Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll
description: Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll
copied-description: true
exl-id: 56004a0f-118c-42f3-869b-2cc1c91ee544
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Tillåtelselista för Adobe® Primetime-program som kan spela upp skyddat innehåll {#allowlist-for-adobe-primetime-applications-allowed-to-play-protected-content}

Anger vilka AIR/iOS-program som kan spela upp innehåll. Ange program-ID för AIR/iOS, lägsta version, högsta version och utgivar-ID.

Exempel: Använd den här regeln om du vill begränsa uppspelningen till ett visst AIR/iOS-program, eller om du vill styra vilken version som har åtkomst till innehållet.

>[!NOTE]
>
>Om du använder Adobe Flash Builder för att skapa skyddade program ska du se till att du inte distribuerar programmet i felsökningsläge. När du distribuerar ett program i felsökningsläge lägger Flash Builder till .debug i AIR program-ID. Detta kommer att få tillåtelselista i Adobe Access att uppträda oväntat.
