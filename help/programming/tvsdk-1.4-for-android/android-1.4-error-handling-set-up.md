---
description: Skapa en enda plats för att hantera fel.
title: Konfigurera felhantering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Konfigurera felhantering{#set-up-error-handling}

Skapa en enda plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel `MediaPlayerStatusChangeEvent` -objekt.
1. I återanropet, när det returnerade läget är `MediaPlayerState.ERROR`, tillhandahåller logik för att hantera alla fel.
1. När felet har hanterats återställer du `MediaPlayer` eller läsa in en ny medieresurs.

   När `MediaPlayer` objektet är i feltillstånd, det förblir i det läget tills du återställer det med `MediaPlayer.reset` -metod.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Till exempel:

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
