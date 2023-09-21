---
title: Fjärradministration och lokal leverans av iOS-nyckel
description: Fjärradministration och lokal leverans av iOS-nyckel
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Fjärradministration och lokal leverans av iOS-nyckel {#remote-and-local-ios-key-delivery}

Adobe Primetime har stöd för följande alternativ för leverans av nycklar till iOS-klienter:

* **Fjärr** - Utför enligt specifikationen i specifikationen för HTTP-direktuppspelning (HLS). M3U8-manifestet anger en HTTPS-sökväg som innehåller en AES-nyckel som ska användas för att dekryptera följande krypterade segment i strömmen. När du anger `Remote` i Primetimes DRM-princip måste klientenheten ansluta till en HTTPS-fjärrserver för att erhålla en AES-nyckel.

* **Lokal** - När du anger `Local` i Primetime DRM i stället för att ansluta till Internet/nätverk för AES-nyckeln bäddas en lokal HTTPS-server in i iOS-programmet, som sedan hanterar alla AES-nyckelbegäranden. Den inbäddade HTTPS-servern konfigureras automatiskt i P-programmet. Ingen åtgärd krävs av programutvecklaren.

Fjärrnyckelleveransen aktiveras via DRM-principen Primetime som används för att paketera innehåll. Om du vill ändra den här inställningen måste du paketera om innehållet. Om du aktiverar fjärrnyckelleverans måste du distribuera en Primetime DRM-nyckelserver som kan hantera nyckelbegäranden från iOS-klienter. Arbetsflödet för klienter på andra plattformar ändras dock inte.

>[!NOTE]
>
>Valet av nyckelleverans påverkar bara iOS-klienter. Alla andra enheter som använder HLS-innehåll, till exempel Android och Primetime on Desktop (Flash Player), använder alltid `Local` nyckelleverans, även om `Remote` har angetts.
