---
title: Blockeringslista i programkörningar
description: Blockeringslista i programkörningar
copied-description: true
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Blockeringslista i programkörningar {#blocklist-of-application-runtimes}

Blockeringslista i programkörningar anger vilken version av Primetime-klienten eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som Primetime DRM Client blockeringslista kan den senaste versionen av runtimes för Flash Player, AIR och iOS anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Du kan identifiera programkörningen med något av attributen som stöds för Primetime DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Exakt matchning | Identifierar namnet på programkörningen. |
