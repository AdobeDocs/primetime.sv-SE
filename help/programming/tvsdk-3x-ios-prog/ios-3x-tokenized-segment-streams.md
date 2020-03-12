---
description: HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.
seo-description: HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.
seo-title: Tokeniserade segmentströmmar
title: Tokeniserade segmentströmmar
uuid: 62e3b858-2605-4960-b504-9010674f80ad
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Tokeniserade segmentströmmar {#tokenized-segment-streams}

HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.

Tokens som angetts som cookies i huvudmanifestets (m3u8) svar delas inte med segmentförfrågningar, även när segmentförfrågningarna gäller samma domän. Om du vill aktivera delning av dessa cookies i en segmentbegäran anger du följande egenskap för den `PTMetadata` instans som spelarobjektet har:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Ytterligare en begäran görs till huvudmanifestet (m3u8) innan strömmen börjar spelas upp.

>[!IMPORTANT]
>
>Den här funktionen för cookie-delning stöds bara på enheter med iOS 8 eller senare.

