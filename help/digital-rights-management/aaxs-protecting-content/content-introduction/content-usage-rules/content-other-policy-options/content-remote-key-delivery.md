---
title: Fjärr- och lokal nyckelleverans från iOS
description: Fjärr- och lokal nyckelleverans från iOS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Fjärr- och lokal nyckelleverans från iOS{#remote-and-local-ios-key-delivery}

Adobe Primetime har stöd för två alternativ:

* Fjärr - Precis som anges i HLS-specifikationen anger M3U8-manifestet en HTTPS-sökväg som innehåller en AES-nyckel som ska användas för att dekryptera följande krypterade segment i strömmen. När &quot;Fjärr&quot; har angetts kommer klientenheten att nå ut till en fjärr-HTTPS-server för att hämta AES-nyckeln.
* Lokal - När Lokal anges, i stället för att nå ut via Internet/nätverk för AES-nyckeln, bäddas en lokal HTTPS-server in i iOS-programmet som hanterar alla AES-nyckelbegäranden. Den inbäddade HTTPS-servern konfigureras automatiskt i Primetime-programmet. Ingen åtgärd krävs av programutvecklaren.

Fjärrnyckelleveransen aktiveras via den princip som används för att paketera innehåll (om du ändrar den här inställningen måste innehållet paketeras om). När fjärrnyckelleveransen är aktiverad måste en Adobe Access Key Server distribueras för att hantera nyckelbegäranden från iOS-klienter, men arbetsflödet för klienter på andra plattformar ändras inte.

>[!NOTE]
>
>Valet av nyckelleverans påverkar bara iOS-klienter. Alla andra enheter som använder HLS-innehåll använder alltid &quot;lokal&quot; nyckelleverans, även om &quot;fjärr&quot; har angetts.

Mer information finns i *Använda nyckelservern Adobe Access*.
