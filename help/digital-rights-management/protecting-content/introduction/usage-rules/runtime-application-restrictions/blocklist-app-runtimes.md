---
title: Blockeringslista i programkörningar
description: Blockeringslista i programkörningar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Blockeringslista i programkörningar {#blocklist-of-application-runtimes}

Blockeringslista i programkörningar anger vilken version av Primetime-klienten eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel på användningsfall: Precis som blockeringslista för Primetime DRM Client kan den senaste versionen av Flashen Player, AIR eller iOS anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Du kan identifiera programkörningen med något av attributen som stöds för Primetime DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Exakt matchning | Identifierar namnet på programkörningen. |
