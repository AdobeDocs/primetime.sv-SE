---
seo-title: Fjärradministration och lokal leverans av iOS-nycklar
title: Fjärradministration och lokal leverans av iOS-nycklar
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Fjärradministration och lokal leverans av iOS-nycklar {#remote-and-local-ios-key-delivery}

Adobe Primetime har stöd för följande alternativ för leverans av nycklar till iOS-klienter:

* **Fjärr** - Utför enligt specifikationen i HTTP Live Streaming (HLS)-specifikationen. M3U8-manifestet anger en HTTPS-sökväg som innehåller en AES-nyckel som ska användas för att dekryptera följande krypterade segment i strömmen. När du anger detta `Remote` i DRM-principen måste klientenheten ansluta till en HTTPS-fjärrserver för att få en AES-nyckel.

* **Lokal** - När du anger detta `Local` i Primetime DRM i stället för att ansluta till Internet/nätverk för AES-nyckeln, bäddas en lokal HTTPS-server in i iOS-programmet, som sedan hanterar alla AES-nyckelbegäranden. Den inbäddade HTTPS-servern konfigureras automatiskt i P-programmet. Ingen åtgärd krävs av programutvecklaren.

Fjärrnyckelleveransen aktiveras via DRM-principen Primetime som används för att paketera innehåll. Om du vill ändra den här inställningen måste du paketera om innehållet. Om du aktiverar fjärrnyckelleverans måste du distribuera en Primetime DRM-nyckelserver som kan hantera nyckelbegäranden från iOS-klienter. Arbetsflödet för klienter på andra plattformar ändras dock inte.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Val av nyckelleverans påverkar bara iOS-klienter. Alla andra enheter som använder HLS-innehåll, till exempel Android och Primetime on Desktop (Flash Player), använder alltid `Local` nyckelleverans, även om det `Remote` har angetts.

