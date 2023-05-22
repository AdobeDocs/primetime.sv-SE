---
description: TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.
title: API-element för prisändring
exl-id: deb8c1cb-c6b2-4328-a5e1-cca893ea066f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# API-element för prisändring {#rate-change-api-elements}

TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Använd följande API-element om du vill ändra uppspelningsfrekvensen:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, som anger giltiga frekvenser.

| Kursens värde | Effekt vid uppspelning |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Växlar till snabbläge med den angivna multiplikatorn snabbare än normalt (4 är till exempel 4 gånger snabbare än normalt) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Växlar till snabbspolningsläge |
| 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är detsamma som att ställa in egenskapen rate på 1.0) |
| 0.0 | Pausar (anropar `pause` är detsamma som att ställa in egenskapen rate på 0,0) |
