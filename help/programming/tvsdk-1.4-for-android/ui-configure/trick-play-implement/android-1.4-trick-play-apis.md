---
description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som rör snabb framåtspolning och tillbakaspolning.
title: API-element för prisändring
exl-id: 9c366645-5ce5-485c-8423-cb0ed4bd2677
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# API-element för prisändring{#rate-change-api-elements}

TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som rör snabb framåtspolning och tillbakaspolning.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Använd följande API-element om du vill ändra uppspelningsfrekvensen:

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
| 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är detsamma som att ställa in egenskapen rate på 1.0) |
| 0.0 | Pausar (anropar `pause` är detsamma som att ställa in egenskapen rate på 0,0) |
