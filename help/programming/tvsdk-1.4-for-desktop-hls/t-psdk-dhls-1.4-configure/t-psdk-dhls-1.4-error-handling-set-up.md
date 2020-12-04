---
description: Skapa en enda plats för att hantera fel.
seo-description: Skapa en enda plats för att hantera fel.
seo-title: Konfigurera felhantering
title: Konfigurera felhantering
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# Konfigurera felhantering{#set-up-error-handling}

Skapa en enda plats för att hantera fel.

1. Implementera en händelseåteranropsfunktion för `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK skickar händelseinformation, till exempel ett `MediaPlayerStatusChangeEvent`-objekt.
1. I återanropet, när statusen från händelseparametern är `MediaPlayerStatus.ERROR`, tillhandahåller du logik för att hantera alla fel.
1. När felet har hanterats återställer du objektet `MediaPlayer` eller läser in en ny medieresurs.

   När `MediaPlayer`-objektet är i feltillstånd kan det inte avsluta det här läget förrän du antingen återställer `MediaPlayer`-objektet (via metoden `MediaPlayer.reset`) eller läser in en ny medieresurs ( `MediaPlayer.replaceCurrentItem`).

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

