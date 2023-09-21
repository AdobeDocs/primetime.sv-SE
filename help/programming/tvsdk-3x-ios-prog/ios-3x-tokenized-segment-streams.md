---
description: HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.
title: Tokeniserade segmentströmmar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Tokeniserade segmentströmmar {#tokenized-segment-streams}

HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.

Tokens som angetts som cookies i huvudmanifestets (m3u8) svar delas inte med segmentförfrågningar, även när segmentförfrågningarna gäller samma domän. Om du vill aktivera delning av dessa cookies i en segmentbegäran anger du följande egenskap på `PTMetadata` -instans som har angetts för spelarobjektet: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Ytterligare en begäran görs till huvudmanifestet (m3u8) innan strömmen börjar spelas upp.

>[!IMPORTANT]
>
>Den här funktionen för cookie-delning stöds bara på enheter med iOS 8 eller senare.
