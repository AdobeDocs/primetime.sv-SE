---
description: 'null'
seo-description: 'null'
seo-title: Lista över programkörningar
title: Lista över programkörningar
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista över programkörningar{#blacklist-of-application-runtimes}

En svartlista över programkörningar anger vilken version av Primetime-klienten eller Flash-miljön som inte har åtkomst till innehållet. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: Precis som i Primetimes svartlista över DRM-klienter kan den senaste versionen av Flash Player-, AIR- eller iOS-runtimes anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Du kan identifiera programkörningen med något av attributen som stöds för Primetime DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Exakt matchning | Identifierar namnet på programkörningen. |

