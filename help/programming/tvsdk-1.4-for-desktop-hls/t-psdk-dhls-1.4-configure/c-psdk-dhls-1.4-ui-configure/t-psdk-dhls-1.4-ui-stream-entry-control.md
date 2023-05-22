---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).
title: Ange en ström vid en viss tidpunkt
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Ange en ström vid en viss tidpunkt{#enter-a-stream-at-a-specific-time}

Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).

Skicka en position till `MediaPlayer.prepareToPlay`.

TVSDK anser att den angivna positionen är utgångspunkten för tillgången. Ingen sökåtgärd krävs. Om positionen inte ligger inom det sökbara intervallet använder standardpositionen.

Till exempel:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
