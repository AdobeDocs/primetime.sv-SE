---
description: Du kan konfigurera en plats för att hantera fel.
seo-description: Du kan konfigurera en plats för att hantera fel.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: 7c122830-6259-4e95-882e-fb1700454e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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
