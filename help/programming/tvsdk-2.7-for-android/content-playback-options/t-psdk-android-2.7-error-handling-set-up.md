---
description: Du kan konfigurera en plats för att hantera fel.
seo-description: Du kan konfigurera en plats för att hantera fel.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Konfigurera felhantering {#set-up-error-handling}

Du kan konfigurera en plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel ett `MediaPlayerStatusChangeEvent` objekt.
1. I callback-funktionen, när den returnerade statusen är `MediaPlayerStatus.ERROR`, tillhandahåller du logik för att hantera alla fel.
1. Återställ objektet eller läs in en ny medieresurs när felet har hanterats. `MediaPlayer`

   När `MediaPlayer` objektet har felstatusen förblir det i den statusen tills du återställer det med `MediaPlayer.reset` metoden.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

Exempel:

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```

