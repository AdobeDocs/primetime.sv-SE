---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).
seo-description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).
seo-title: Ange en ström vid en viss tidpunkt
title: Ange en ström vid en viss tidpunkt
uuid: f58d908a-77b9-465f-b3a9-8fe63a249d39
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 1%

---


# Ange en ström vid en viss tidpunkt{#enter-a-stream-at-a-specific-time}

Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).

Skicka en position till `MediaPlayer.prepareToPlay`.

TVSDK anser att den angivna positionen är utgångspunkten för tillgången. Ingen sökåtgärd krävs. Om positionen inte ligger inom det sökbara intervallet använder standardpositionen.

Exempel:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
