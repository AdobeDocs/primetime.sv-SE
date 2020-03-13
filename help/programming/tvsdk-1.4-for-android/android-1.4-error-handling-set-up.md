---
description: Skapa en enda plats för att hantera fel.
seo-description: Skapa en enda plats för att hantera fel.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Konfigurera felhantering{#set-up-error-handling}

Skapa en enda plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel ett `MediaPlayerStatusChangeEvent` objekt.
1. I callback-funktionen, när det returnerade läget är `MediaPlayerState.ERROR`, tillhandahåller du logik för att hantera alla fel.
1. Återställ objektet eller läs in en ny medieresurs när felet har hanterats. `MediaPlayer`

   När `MediaPlayer` objektet är i feltillstånd förblir det i det läget tills du återställer det med `MediaPlayer.reset` metoden.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Exempel:

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```

