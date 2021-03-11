---
title: Blockeringslista i programkörningar
description: Blockeringslista i programkörningar
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Blockeringslista i programkörningsmiljöerna {#blocklist-of-application-runtimes}

Blockeringslista i programkörningar anger vilken version av Primetime-klienten eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som Primetime DRM Client blockeringslista kan den senaste versionen av Flash Player, AIR eller iOS anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Du kan identifiera programkörningen med något av attributen som stöds för Primetime DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Exakt matchning | Identifierar namnet på programkörningen. |

