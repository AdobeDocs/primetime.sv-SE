---
title: Förhandsladda licenser för uppspelning offline - översikt
description: Förhandsladda licenser för uppspelning offline - översikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Läser in licenser i förväg för uppspelning offline {#pre-loading-licenses-for-offline-playback}

Du kan förhandsladda de licenser som krävs för att spela upp innehåll som skyddas av Primetime DRM. Med förinlästa licenser kan användarna visa innehållet oavsett om de har en aktiv Internetanslutning eller inte.

Själva förinläsningsprocessen *kräver en Internetanslutning.*. Du kan använda `DRMManager.loadVoucher()` i förväg för att läsa in licenser i förväg. När klienten senare vill spela upp önskat innehåll har DRM-systemet förinstallerats och kan spela upp det skyddade innehållet direkt.
