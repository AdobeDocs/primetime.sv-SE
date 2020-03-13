---
seo-title: Fjärradministration och lokal leverans av iOS-nycklar
title: Fjärradministration och lokal leverans av iOS-nycklar
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Fjärradministration och lokal leverans av iOS-nycklar{#remote-and-local-ios-key-delivery}

Adobe Primetime har stöd för två alternativ för leverans av nycklar till iOS-klienter:

* Fjärr - Precis som anges i HLS-specifikationen anger M3U8-manifestet en HTTPS-sökväg som innehåller en AES-nyckel som ska användas för att dekryptera följande krypterade segment i strömmen. När &quot;Fjärr&quot; har angetts kommer klientenheten att nå ut till en fjärr-HTTPS-server för att hämta AES-nyckeln.
* Lokal - När Lokal anges, i stället för att nå ut via Internet/nätverk för AES-nyckeln, bäddas en lokal HTTPS-server in i iOS-programmet som hanterar alla AES-nyckelbegäranden. Den inbäddade HTTPS-servern konfigureras automatiskt i Primetime-programmet. Ingen åtgärd krävs av programutvecklaren.

Fjärrnyckelleveransen aktiveras via den princip som används för att paketera innehåll (om den här inställningen ändras måste innehållet paketeras om). När fjärrnyckelleveransen är aktiverad måste en Adobe Access Key Server distribueras för att hantera nyckelbegäranden från iOS-klienter, men arbetsflödet för klienter på andra plattformar ändras inte.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Val av nyckelleverans påverkar bara iOS-klienter. Alla andra enheter som använder HLS-innehåll använder alltid &quot;lokal&quot; nyckelleverans, även om &quot;fjärr&quot; har angetts.

Mer information finns i *Använda nyckelservern* för Adobe Access.
