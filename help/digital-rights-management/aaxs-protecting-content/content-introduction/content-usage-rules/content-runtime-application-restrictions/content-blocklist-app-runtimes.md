---
title: Blockeringslista i programkörningsmiljön hindras från att komma åt skyddat innehåll
description: Blockeringslista i programkörningsmiljön hindras från att komma åt skyddat innehåll
copied-description: true
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Blockeringslista i programkörningsmiljön hindras från att komma åt skyddat innehåll {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Anger den version av Primetime eller Flash Runtime som inte har åtkomst till innehåll. Ange begränsad körningsmiljö (Flash Player, AIR eller iOS), plattform och version.

Exempel: Precis som för DRM Client blockeringslista kan den senaste versionen av runtimes för Flash Player, AIR och iOS anges som den lägsta version som krävs för hämtning av licenser och uppspelning av innehåll.

Programkörningen kan identifieras av något av attributen som stöds för DRM-klientversioner, förutom följande attribut:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Program | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Exakt matchning | Identifierar namnet på programkörningen. |
