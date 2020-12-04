---
seo-title: Förhandsladda licenser för uppspelning offline - översikt
title: Förhandsladda licenser för uppspelning offline - översikt
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Läser in licenser i förväg för uppspelning offline {#pre-loading-licenses-for-offline-playback}

Du kan förhandsladda de licenser som krävs för att spela upp innehåll som skyddas av Primetime DRM. Med förinlästa licenser kan användarna visa innehållet oavsett om de har en aktiv Internetanslutning eller inte.

Själva förinläsningsprocessen *kräver en Internetanslutning.*. Du kan använda `DRMManager.loadVoucher()` i förväg för att läsa in licenser i förväg. När klienten senare vill spela upp önskat innehåll har DRM-systemet förinstallerats och kan spela upp det skyddade innehållet direkt.
