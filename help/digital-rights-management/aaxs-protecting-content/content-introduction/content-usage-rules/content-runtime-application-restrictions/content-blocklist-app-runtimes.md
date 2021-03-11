---
title: Blockeringslista i programkörningsmiljön hindras från att komma åt skyddat innehåll
description: Blockeringslista i programkörningsmiljön hindras från att komma åt skyddat innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Blockeringslista i programkörningsmiljön hindrades från att komma åt skyddat innehåll {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Anger den version av Primetime eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: På samma sätt som för DRM Client blockeringslista kan den senaste versionen av Flash Player, AIR eller iOS anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Programkörningen kan identifieras av något av attributen som stöds för DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Exakt matchning | Identifierar namnet på programkörningen. |
