---
title: Förhandsladda licenser för uppspelning offline - översikt
description: Förhandsladda licenser för uppspelning offline - översikt
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Förinläsning av licenser för uppspelning offline {#pre-loading-licenses-for-offline-playback}

Du kan förhandsladda de licenser som krävs för att spela upp innehåll som skyddas av Primetime DRM. Med förinlästa licenser kan användarna visa innehållet oavsett om de har en aktiv Internetanslutning eller inte.

Själva förinläsningsprocessen *gör* kräver en Internetanslutning. Du kan använda `DRMManager.loadVoucher()` i förväg ladda licenser. När klienten senare vill spela upp önskat innehåll har DRM-systemet förinstallerats och kan spela upp det skyddade innehållet direkt.
