---
seo-title: Lista med programkörningsmiljöer som inte har åtkomst till skyddat innehåll
title: Lista med programkörningsmiljöer som inte har åtkomst till skyddat innehåll
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista med programkörningsmiljöer som inte har åtkomst till skyddat innehåll {#blacklist-of-application-runtimes-restricted-from-accessing-protected-content}

Anger den version av Primetime eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som svartlistan över DRM-klienter kan den senaste versionen av Flash Player-, AIR- eller iOS-runtimes anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Programkörningen kan identifieras av något av attributen som stöds för DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Exakt matchning | Identifierar namnet på programkörningen. |

