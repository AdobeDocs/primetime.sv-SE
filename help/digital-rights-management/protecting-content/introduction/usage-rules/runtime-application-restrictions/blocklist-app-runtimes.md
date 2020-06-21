---
description: 'null'
seo-description: 'null'
seo-title: Blockera lista över programkörningar
title: Blockera lista över programkörningar
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Blockera lista över programkörningar{#blocklist-of-application-runtimes}

Blocklista med programkörningar anger vilken version av Primetime-klienten eller Flash Runtime som inte har åtkomst till innehållet. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som i listan över DRM-klientblock i Primetime kan den senaste versionen av Flash Player-, AIR- eller iOS-runtimes anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Du kan identifiera programkörningen med något av attributen som stöds för Primetime DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Exakt matchning | Identifierar namnet på programkörningen. |

