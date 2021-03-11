---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).
title: Ange en ström vid en viss tidpunkt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

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
