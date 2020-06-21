---
seo-title: Blockera en lista över programkörningsmiljöer som inte har åtkomst till skyddat innehåll
title: Blockera en lista över programkörningsmiljöer som inte har åtkomst till skyddat innehåll
uuid: 462a2c09-b335-4768-bd0e-1359db169d69
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Blockera en lista över programkörningsmiljöer som inte har åtkomst till skyddat innehåll {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Anger den version av Primetime eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som med blockeringslistan för DRM-klienten kan den senaste versionen av Flash Player-, AIR- eller iOS-runtimes anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Programkörningen kan identifieras av något av attributen som stöds för DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Exakt matchning | Identifierar namnet på programkörningen. |

