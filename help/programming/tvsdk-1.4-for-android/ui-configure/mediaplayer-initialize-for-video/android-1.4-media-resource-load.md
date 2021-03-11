---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
title: Läsa in en medieresurs i MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Läs in en medieresurs i MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.

1. Ställ in MediaPlayers uppspelningsbara objekt med den nya resurs som ska spelas upp.

   Ersätt det befintliga MediaPlayers uppspelningsbara objekt genom att anropa `MediaPlayer.replaceCurrentItem` och skicka en befintlig `MediaResource`-instans.

1. Registrera en implementering av gränssnittet `MediaPlayer.PlaybackEventListener` med instansen `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`och kontrollera om det finns INITIALIZED och ERROR.

1. När mediespelarens tillstånd ändras till INITIALIZED kan du anropa `MediaPlayer.prepareToPlay`

   Initieringstillståndet anger att mediet har lästs in. Om du anropar `prepareToPlay` startar du annonsupplösningen och placeringsprocessen, om det finns någon.

1. När TVSDK anropar återanropet `onPrepared` har medieströmmen lästs in och förbereds för uppspelning.

   När medieströmmen läses in skapas en `MediaPlayerItem`.

>Om ett fel inträffar växlar `MediaPlayer` till FELstatus. Programmet meddelas också genom att du anropar `PlaybackEventListener.onStateChanged`callback-funktionen.
>
>Detta skickar flera parametrar:
>* En `state`-parameter av typen `MediaPlayer.PlayerState` med värdet `MediaPlayer.PlayerState.ERROR`.
   >
   >
* En `notification`-parameter av typen `MediaPlayerNotification` som innehåller diagnostikinformation om felhändelsen.


Följande förenklade exempelkod visar processen för inläsning av en medieresurs:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
