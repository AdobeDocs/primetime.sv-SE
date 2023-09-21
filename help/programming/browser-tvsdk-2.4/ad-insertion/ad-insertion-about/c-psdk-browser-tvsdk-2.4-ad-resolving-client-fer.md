---
description: FER-innehåll (Full Event Replay) är ett direktflöde som konverteras till VOD genom att taggen
title: FER, lösning och infogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# FER, lösning och infogning{#fer-ad-resolving-and-insertion}

FER-innehåll (Full Event Replay) är ett direktflöde som konverteras till VOD genom att taggen #EXT-X-ENDLIST läggs till i slutet av manifestfilen. Strömmen behåller sina annonsmarkörer.

Webbläsare-TVSDK hanterar en FER-ström som VOD, så som standard är annonsljudläget `SERVER_MAP`. Men eftersom dataströmmen behåller sina annonsmarkörer kan du ange att annonssigneringsläget ska vara `MANIFEST_CUES`som gör att du kan använda annonsmarkörerna för annonsinfogning.

Så här aktiverar du annonsinfogning med markörer för en FER-ström:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER-annonsupplösning och infogningsbeteende liknar live-annonsupplösning och infogning. Webbläsare-TVSDK gör följande:

1. Infogar alla förrollsannonser i början av innehållet.
1. Åtgärdar annonser som anges av referenspunkterna som definieras i manifestet.
1. Ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet
1. Beräknar om den virtuella tidslinjen, om det behövs.

**Begränsning:** Webbläsarens TVSDK stöder bara uppspelning av HLS FER-strömmar. MP4-annonser på mellannivå stöds inte heller med FER-strömmar.
