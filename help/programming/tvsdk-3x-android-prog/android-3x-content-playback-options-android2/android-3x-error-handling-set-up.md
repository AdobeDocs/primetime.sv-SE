---
description: Du kan konfigurera en plats för att hantera fel.
title: Konfigurera felhantering
exl-id: 9b83b47e-6d30-452b-87c3-1e3a139f2e69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Konfigurera felhantering {#set-up-error-handling}

Du kan konfigurera en plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel `MediaPlayerStatusChangeEvent` -objekt.
1. I återanropet, när den returnerade statusen är `MediaPlayerStatus.ERROR`, tillhandahåller logik för att hantera alla fel.
1. När felet har hanterats återställer du `MediaPlayer` eller läsa in en ny medieresurs.

   När `MediaPlayer` objektet har felstatus och behålls i den statusen tills du återställer det med `MediaPlayer.reset` -metod.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

Till exempel:

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
