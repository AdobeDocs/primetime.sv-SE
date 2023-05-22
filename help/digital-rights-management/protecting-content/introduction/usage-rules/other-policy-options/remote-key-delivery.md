---
title: Fjärradministration och lokal leverans av iOS-nycklar
description: Fjärradministration och lokal leverans av iOS-nycklar
copied-description: true
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Fjärradministration och lokal leverans av iOS-nycklar {#remote-and-local-ios-key-delivery}

Adobe Primetime har stöd för följande alternativ för nyckelleverans till iOS-klienter:

* **Fjärr** - Utför enligt specifikationen i HTTP Live Streaming (HLS)-specifikationen. M3U8-manifestet anger en HTTPS-sökväg som innehåller en AES-nyckel som ska användas för att dekryptera följande krypterade segment i strömmen. När du anger `Remote` i Primetimes DRM-princip måste klientenheten ansluta till en HTTPS-fjärrserver för att erhålla en AES-nyckel.

* **Lokal** - När du anger `Local` i Primetime DRM i stället för att ansluta till Internet/nätverk för AES-nyckeln bäddas en lokal HTTPS-server in i iOS-programmet, som sedan hanterar alla AES-nyckelbegäranden. Den inbäddade HTTPS-servern konfigureras automatiskt i P-programmet. Ingen åtgärd krävs av programutvecklaren.

Fjärrnyckelleveransen aktiveras via DRM-principen Primetime som används för att paketera innehåll. Om du vill ändra den här inställningen måste du paketera om innehållet. Om du aktiverar fjärrnyckelleverans måste du distribuera en Primetime DRM Key Server som kan hantera nyckelbegäranden från iOS-klienter. Arbetsflödet för klienter på andra plattformar ändras dock inte.

>[!NOTE]
>
>Valet av nyckelleverans påverkar bara iOS-klienter. Alla andra enheter som använder HLS-innehåll, till exempel Android och Primetime på skrivbordet (Flash Player), använder alltid `Local` nyckelleverans, även om `Remote` har angetts.
