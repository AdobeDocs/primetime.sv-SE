---
description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
title: Implementera snabbt framåt och bakåt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Implementera snabbt framåt och bakåt{#implement-fast-forward-and-rewind}

När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.

>[!IMPORTANT]
>
>* Trick play-läge stöds bara för MPEG Dash- och HLS VOD-innehåll.
>* Trick play-läge stöds inte för liveströmmar eller annonser.
>* När du byter från huvudinnehåll till en annons lämnar Browser TVSDK trickläget.
>

Om du vill växla hastighet måste du ange ett värde.

1. Gå från normalt uppspelningsläge (1x) till uppspelningsläge genom att ställa in hastigheten på `MediaPlayer` till ett tillåtet värde.

   * The `MediaPlayerItem` -klassen definierar de tillåtna uppspelningshastigheterna.
   * Webbläsarens TVSDK väljer den närmaste tillåtna hastigheten om den angivna hastigheten inte tillåts.

     Följande exempelfunktion ställer in hastigheten:

     ```js
     setTrickPlayRate = function (player, trickPlayRate) { 
                   player.rate = trickPlayRate; 
     }
     ```

     Följande exempelfunktion kan användas för att ställa frågor om tillgängliga uppspelningshastigheter:

     ```js
     getAvailableTrickPlayRates = function (player) { 
              var item = player.currentItem; 
              var availableRates = item. availablePlaybackRates; 
              return availableRates; 
     } 
     ```

1. Du kan avlyssna ränteförändringshändelser, som du får veta när du har begärt en tariffändring och när en prisändring faktiskt inträffar.

       Webbläsarens TVSDK skickar följande händelser som är relaterade till trick play:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` när `rate` värdet ändras till ett annat värde.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` när uppspelningen återupptas med vald hastighet.

     Webbläsarens TVSDK skickar båda dessa händelser när spelaren återgår från trippelläge till normalt uppspelningsläge.

## API-element för prisändring {#rate-change-API-elements}

Webbläsarens TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga hastigheter, aktuella hastigheter, om tricks-play stöds och andra funktioner för snabb framåtspolning och tillbakaspolning.

Använd följande API-element om du vill ändra uppspelningsfrekvensen:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - anger giltiga frekvenser.

  | Kursens värde | Effekt vid uppspelning |
  |---|---|
  | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Växlar till snabbläge med den angivna multiplikatorn snabbare än normalt (4 gånger snabbare än normalt) |
  | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Växlar till snabbspolningsläge |
  | 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är detsamma som att ställa in egenskapen rate på 1.0) |
  | 0.0 | Pausar (anropar `pause` är detsamma som att ställa in egenskapen rate på 0,0) |

## Begränsningar och beteenden för trick-play {#limitations-and-behavior-trick-play}

Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.

Här är en lista över begränsningarna för trippelläge:

* Om strömmen inte innehåller någon trippelpassning inaktiveras snabb tillbakaspolning och den maximala uppspelningshastigheten för snabb framåtspolning begränsas till 8.
* När tricks-play-anpassningar används för att tillhandahålla trickläget inaktiveras ljudspåret.
* I trippelläge är växling av ljudspår och spår för stängda bildtexter inaktiverat.
* Uppspelning och paus är aktiverat.
* Vid sökning, om uppspelningen är i trippelläge, ställs uppspelningshastigheten in på 1 och den normala uppspelningen återupptas.
* Logiken för adaptiv bithastighet (ABR) är aktiverad.

  När du använder normala anpassningar begränsas profilerna mellan `ABRControlParameters.minBitRate` och `ABRControlParameters.maxBitRate`. När du använder trippelanpassningar begränsas profilerna mellan `ABRControlParameters.minTrickPlayBitRate` och `ABRControlParameters.maxTrickPlayBitRate`.
