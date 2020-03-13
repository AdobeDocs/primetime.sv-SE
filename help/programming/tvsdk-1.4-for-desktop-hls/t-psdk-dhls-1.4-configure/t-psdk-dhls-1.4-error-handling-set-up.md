---
description: Skapa en enda plats för att hantera fel.
seo-description: Skapa en enda plats för att hantera fel.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Konfigurera felhantering{#set-up-error-handling}

Skapa en enda plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel ett `MediaPlayerStatusChangeEvent` objekt.
1. I återanropet, när status från händelseparametern är `MediaPlayerStatus.ERROR`, tillhandahåller du logik för att hantera alla fel.
1. Återställ objektet eller läs in en ny medieresurs när felet har hanterats. `MediaPlayer`

   När `MediaPlayer` objektet är i feltillstånd kan det inte avsluta det här läget förrän du antingen återställer `MediaPlayer` objektet (via `MediaPlayer.reset` metoden) eller läser in en ny medieresurs ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Exempel:

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

