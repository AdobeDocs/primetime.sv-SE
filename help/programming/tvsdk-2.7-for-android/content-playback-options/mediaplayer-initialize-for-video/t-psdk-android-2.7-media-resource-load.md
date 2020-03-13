---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-title: Läsa in en medieresurs i mediespelaren
title: Läsa in en medieresurs i mediespelaren
uuid: 0334fa69-1d92-44d8-8891-2bc90a1ea498
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Läsa in en medieresurs i mediespelaren {#load-a-media-resource-in-the-media-player}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.

1. Ställ in mediespelaren så att den spelar upp den nya resursen.

   Ersätt det objekt som spelas upp just nu genom att anropa `MediaPlayer.replaceCurrentResource()` och skicka en befintlig `MediaResource` instans.

   Detta startar resursinläsningsprocessen.

1. Registrera `MediaPlayerEvent.STATUS_CHANGED` händelsen med `MediaPlayer` instansen. Kontrollera om det finns minst följande statusvärden i återanropet:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   Genom de här händelserna meddelar `MediaPlayer` objektet programmet när mediaresursen har lästs in.
1. När statusen för mediespelaren ändras till `INITIALIZED`kan du ringa `MediaPlayer.prepareToPlay()`.

   Den här statusen anger att mediet har lästs in. Det nya `MediaPlayerItem` är klart för uppspelning. Anrop `prepareToPlay()` startar upplösningen av annonsen och placeringsprocessen, om det finns någon.

Om ett fel inträffar växlar mediespelaren till `ERROR` status.

Följande förenklade exempelkod visar processen för inläsning av en medieresurs:
>```java>
>// mediaResource is a properly configured MediaResource instance 
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
