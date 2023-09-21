---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (DefaultMediaPlayer.LIVE_POINT).
title: Ange en ström vid en viss tidpunkt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
