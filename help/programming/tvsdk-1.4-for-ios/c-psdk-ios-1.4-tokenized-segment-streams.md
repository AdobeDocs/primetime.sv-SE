---
description: HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.
seo-description: HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.
seo-title: Tokeniserade segmentströmmar
title: Tokeniserade segmentströmmar
uuid: b17bb5bc-2029-4113-ac44-b1d30aa08ca6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Tokeniserade segmentströmmar{#tokenized-segment-streams}

HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering. Dessa variabler kan anges som URL-parametrar eller som cookie-rubriker.

Tokens som angetts som cookies i det överordnad manifestsvaret (m3u8) delas inte med segmentförfrågningar, även när segmentförfrågningarna gäller samma domän. Om du vill aktivera delning av dessa cookies i en segmentbegäran anger du följande egenskap för `PTMetadata`-instansen som tillhandahålls till spelarobjektet: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Ytterligare en begäran görs till det överordnad manifestet (m3u8) innan strömmen börjar spelas upp.

>[!IMPORTANT]
>
>Den här funktionen för cookie-delning stöds bara på enheter med iOS 8 eller senare.

