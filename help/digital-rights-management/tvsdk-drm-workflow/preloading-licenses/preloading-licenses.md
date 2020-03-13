---
seo-title: Förhandsladda licenser för uppspelning offline - översikt
title: Förhandsladda licenser för uppspelning offline - översikt
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e

---


# Förinläsning av licenser för uppspelning offline {#pre-loading-licenses-for-offline-playback}

Du kan förhandsladda de licenser som krävs för att spela upp innehåll som skyddas av Primetime DRM. Med förinlästa licenser kan användarna visa innehållet oavsett om de har en aktiv Internetanslutning eller inte.

Själva förinläsningsprocessen *kräver* en Internetanslutning. Du kan använda licenserna `DRMManager.loadVoucher()` i förväg. När klienten senare vill spela upp önskat innehåll har DRM-systemet förinstallerats och kan spela upp det skyddade innehållet direkt.
