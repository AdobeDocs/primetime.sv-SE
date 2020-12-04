---
description: När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.
seo-description: När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.
seo-title: Pausa och återuppta uppspelning
title: Pausa och återuppta uppspelning
uuid: a8fec392-3a71-4086-abf1-23522d023680
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Pausa och återuppta uppspelning {#pause-and-resume-playback}

När en användare klickar på en annons bör programmet pausa uppspelningen av huvudvideoinnehållet.

Åsidosätt `onPause` och `onResume` från Android-aktiviteten.

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```

