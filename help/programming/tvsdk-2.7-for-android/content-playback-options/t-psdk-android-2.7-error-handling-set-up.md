---
description: Du kan konfigurera en plats för att hantera fel.
title: Konfigurera felhantering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 2%

---


# Konfigurera felhantering {#set-up-error-handling}

Du kan konfigurera en plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel ett `MediaPlayerStatusChangeEvent`-objekt.
1. I återanropet, när den returnerade statusen är `MediaPlayerStatus.ERROR`, anger du logik för att hantera alla fel.
1. När felet har hanterats återställer du objektet `MediaPlayer` eller läser in en ny medieresurs.

   När `MediaPlayer`-objektet har felstatusen behålls det i den statusen tills du återställer det med metoden `MediaPlayer.reset`.

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

