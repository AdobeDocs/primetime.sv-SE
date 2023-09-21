---
description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
title: Implementera snabbt framåt och bakåt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Implementera snabbt framåt och bakåt {#implement-fast-forward-and-rewind}

När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.

Om du vill växla hastighet måste du ange ett värde.

1. Gå från normalt uppspelningsläge (1x) till uppspelningsläge genom att ställa in `rate` -egenskapen på `MediaPlayer` till ett tillåtet värde.

   * The `MediaPlayerItem` -klassen definierar de tillåtna uppspelningshastigheterna.
   * TVSDK väljer den närmaste tillåtna hastigheten om den angivna hastigheten inte tillåts.

     När trickfrekvensen ändras från 0 (paus) eller 1 (normal uppspelning) till en hastighet som är större än 1 eller mindre än -1 tas alla annonser på tidslinjen bort. Det finns bara en period på hela tidslinjen som underlättar en trickåtgärd för att innehållet ska kunna vidarebefordras och lindras snabbt utan att stanna vid någon annonsposition. Den här åtgärden aktiveras av en åtgärd för att ta bort alla lösta annonsbrytningar på tidslinjen i TVSDK. När trickspelet återupptas vid 0 eller 1 återställs annonsbrytningarna först av åtgärden för att bifoga en tidslinje.

     Kom ihåg följande information:

   * Om trickåtgärden är att spola tillbaka innehållet återupptas uppspelningen när hastigheten ändras till 1.
   * Om trickåtgärden är att snabbspola fram innehållet spelas den senast hoppade annonsen upp vid meritpositionen.

   I det här exemplet ställs spelarens interna uppspelningshastighet in på den begärda hastigheten.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Du kan avlyssna ränteförändringshändelser, som du får veta när du har begärt en tariffändring och när en prisändring faktiskt inträffar.

   TVSDK skickar följande händelser som är relaterade till trick play:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` när `rate` värdet ändras till ett annat värde.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` när uppspelningen återupptas med vald hastighet.

   TVSDK skickar båda dessa händelser när spelaren återgår från trippelläge till normalt uppspelningsläge.

## API-element för prisändring {#rate-change-api}

TVSDK innehåller metoder, egenskaper och händelser för att fastställa giltiga frekvenser, aktuella frekvenser, om trippelning stöds och andra funktioner som är relaterade till snabb framåtspolning och tillbakaspolning.

Använd följande API-element om du vill ändra uppspelningsfrekvensen:

* `MediaPlayer.rate` egenskap med set- och getter-funktioner
* `MediaPlayer.localTime property` med get-funktion
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` egenskap med get-funktion
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` egenskap med get-funktion - anger giltiga frekvenser.

| Kursens värde | Effekt vid uppspelning |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | Växlar till snabbläge med den angivna multiplikatorn snabbare än normalt (4 gånger snabbare än normalt) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | Växlar till snabbspolningsläge |
| 1.0 | Växlar till normalt uppspelningsläge (anrop `play` är detsamma som att ställa in egenskapen rate på 1.0) |
| 0.0 | Pausar (anropar `pause` är detsamma som att ställa in egenskapen rate på 0,0) |

## Begränsningar och beteenden för trick play {#limitations-behavior-trick-play}

Här är begränsningarna för trickläge:

* Huvudspelningslistan måste innehålla segment med bara I-frame. Endast nyckelbildrutorna från I-bildrutespåret visas på skärmen.
* Ljudspåret och undertexter är inaktiverade.
* Logiken för anpassad bithastighet (ABR) är inaktiverad. TVSDK väljer en bithastighet mellan den lägsta angivna hastigheten och 800 kbit/s och använder den hastigheten under hela uppspelningssessionen.
* Uppspelning och paus är aktiverat.
* Sökning tillåts inte. Om du vill söka, ringa `pause` för att avsluta tricks play-läge och sedan ringa `seek`.

* Du kan avsluta trippelläget i valfri tillåten uppspelningshastighet (uppspelning eller paus).
* När annonser har infogats i strömmen:

   * Du kan bara lura att spela medan du spelar huvudinnehållet. Ett fel skickas om du försöker byta för att lura till dig att spela under en annonsbrytning.
   * Efter att tricket har spelats upp ignoreras annonsbrytningar och inga annonshändelser utlöses.
   * Tidslinjen som visas av TVSDK för spelarprogrammet ändras inte även om annonsbrytningar hoppas över.
   * The `MediaPlayer.currentTime` egenskapen hoppar framåt (snabbt framåt) eller bakåt (vid snabb tillbakaspolning) med längden på den överhoppade annonsbrytningen. Detta hoppbeteende för den aktuella tiden gör att strömmens varaktighet förblir oförändrad under trippelning. Spelarprogrammet kan använda `localTime` för att spåra tiden i förhållande enbart till huvudinnehållet. Inga tidshopp utförs för de värden som returneras för lokal tid när en annons hoppas över.

   * The `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` -händelsen skickas omedelbart innan en annonsbrytning kommer att hoppas över. Spelaren kan använda den här händelsen för att implementera anpassad logik som är relaterad till de överhoppade annonsbrytningarna.
   * När du avslutar trick play anropas samma annonsuppspelningsprincip som när sökningen avslutas.

     Som vid sökning beror därför beteendet på om programmets uppspelningsprincip skiljer sig från standardinställningen. Standardinställningen är att den senast hoppade annonsbrytningen spelas upp där du kommer ut ur tricksspelet.
