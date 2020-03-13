---
description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om tricks-play stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.
seo-description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om tricks-play stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.
seo-title: API-element för prisändring
title: API-element för prisändring
uuid: 3554bf45-9419-4740-8a0e-484fc14c7436
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# API-element för prisändring {#rate-change-api-elements}

TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om tricks-play stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Använd följande API-element för att ändra uppspelningsfrekvenser:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, som anger giltiga frekvenser.

| Kursens värde | Effekt vid uppspelning |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Växlar till snabbläge med den angivna multiplikatorn snabbare än normalt (4 är till exempel 4 gånger snabbare än normalt) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Växlar till snabbspolningsläge |
| 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är samma sak som att ställa in egenskapen rate på 1.0) |
| 0.0 | Pausar (anrop `pause` är samma sak som att ställa in egenskapen rate på 0,0) |

