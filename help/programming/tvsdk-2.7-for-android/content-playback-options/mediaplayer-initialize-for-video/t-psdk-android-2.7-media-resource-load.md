---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-title: Läsa in en medieresurs i mediespelaren
title: Läsa in en medieresurs i mediespelaren
uuid: 0334fa69-1d92-44d8-8891-2bc90a1ea498
translation-type: tm+mt
source-git-commit: 67975894814fbed8cfc49764a54b80d123032a49
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Läs in en medieresurs i mediespelaren {#load-a-media-resource-in-the-media-player}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.

1. Ställ in mediespelaren så att den spelar upp den nya resursen.

   Ersätt det uppspelningsbara objektet genom att anropa `MediaPlayer.replaceCurrentResource()` och skicka en befintlig `MediaResource`-instans.

   Detta startar resursinläsningsprocessen.

1. Registrera händelsen `MediaPlayerEvent.STATUS_CHANGED` med instansen `MediaPlayer`. Kontrollera om det finns minst följande statusvärden i återanropet:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   Genom dessa händelser meddelar `MediaPlayer`-objektet ditt program när mediaresursen har lästs in.
1. När mediespelarens status ändras till `INITIALIZED` kan du ringa `MediaPlayer.prepareToPlay()`.

   Den här statusen anger att mediet har lästs in. Den nya `MediaPlayerItem` är klar för uppspelning. Om du anropar `prepareToPlay()` startar du annonsupplösningen och placeringsprocessen, om det finns någon.

Om ett fel inträffar växlar mediespelaren till `ERROR`-status.

Följande förenklade exempelkod visar processen för inläsning av en medieresurs:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```
