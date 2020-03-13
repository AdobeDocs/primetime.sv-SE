---
description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som rör snabb framåtspolning och tillbakaspolning.
seo-description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som rör snabb framåtspolning och tillbakaspolning.
seo-title: API-element för prisändring
title: API-element för prisändring
uuid: 0040d35c-f9cb-4066-9bee-828ed5541194
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# API-element för prisändring{#rate-change-api-elements}

TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som rör snabb framåtspolning och tillbakaspolning.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Använd följande API-element för att ändra uppspelningsfrekvenser:

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` - anger giltiga frekvenser.

| Kursens värde | Effekt vid uppspelning |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Växlar till snabbläge med den angivna multiplikatorn snabbare än normalt (4 är till exempel 4 gånger snabbare än normalt) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Växlar till snabbspolningsläge |
| 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är samma sak som att ställa in egenskapen rate på 1.0) |
| 0.0 | Pausar (anrop `pause` är samma sak som att ställa in egenskapen rate på 0,0) |

