---
description: Skapa en enda plats för att hantera fel.
title: Konfigurera felhantering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Konfigurera felhantering{#set-up-error-handling}

Skapa en enda plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel `MediaPlayerStatusChangeEvent` -objekt.
1. I återanropet, när statusen från händelseparametern är `MediaPlayerStatus.ERROR`, tillhandahåller logik för att hantera alla fel.
1. När felet har hanterats återställer du `MediaPlayer` eller läsa in en ny medieresurs.

   När `MediaPlayer` objektet är i feltillstånd, det kan inte avsluta det här läget förrän du återställer `MediaPlayer` objekt (via `MediaPlayer.reset` eller läsa in en ny medieresurs ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Till exempel:

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```
