---
title: Förhandsladda licenser för uppspelning offline - översikt
description: Förhandsladda licenser för uppspelning offline - översikt
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Förinläsning av licenser för uppspelning offline {#pre-loading-licenses-for-offline-playback}

Du kan förhandsladda de licenser som krävs för att spela upp innehåll som skyddas av Primetime DRM. Med förinlästa licenser kan användarna visa innehållet oavsett om de har en aktiv Internetanslutning eller inte.

Själva förinläsningsprocessen *gör* kräver en Internetanslutning. Du kan använda `DRMManager.loadVoucher()` i förväg ladda licenser. När klienten senare vill spela upp önskat innehåll har DRM-systemet förinstallerats och kan spela upp det skyddade innehållet direkt.
