---
description: 'FER-innehåll (Full Event Replay) är ett direktflöde som konverteras till VOD genom att taggen #EXT-X-ENDLIST läggs till i slutet av manifestfilen. Strömmen behåller sina annonsmarkörer.'
seo-description: 'FER-innehåll (Full Event Replay) är ett direktflöde som konverteras till VOD genom att taggen #EXT-X-ENDLIST läggs till i slutet av manifestfilen. Strömmen behåller sina annonsmarkörer.'
seo-title: FER, lösning och infogning
title: FER, lösning och infogning
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# FER-annonsering löser och infogar{#fer-ad-resolving-and-insertion}

FER-innehåll (Full Event Replay) är ett direktflöde som konverteras till VOD genom att taggen #EXT-X-ENDLIST läggs till i slutet av manifestfilen. Strömmen behåller sina annonsmarkörer.

Webbläsare-TVSDK hanterar en FER-ström som VOD, så som standard är annonslingsläget `SERVER_MAP`. Men eftersom flödet behåller sina annonsmarkörer kan du ställa in annonssignaleringsläget på `MANIFEST_CUES`, vilket gör att du kan använda annonsmarkörerna för annonsinfogning.

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

**Begränsning:** Webbläsarens TVSDK stöder endast uppspelning av HLS FER-strömmar. MP4-annonser på mellannivå stöds inte heller med FER-strömmar.
