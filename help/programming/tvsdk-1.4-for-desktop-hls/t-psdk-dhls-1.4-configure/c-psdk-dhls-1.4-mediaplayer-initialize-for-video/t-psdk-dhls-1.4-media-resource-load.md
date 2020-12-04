---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.
seo-title: Läsa in en medieresurs i MediaPlayer
title: Läsa in en medieresurs i MediaPlayer
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: 84924d84bfa436a8807c2e8d74d1dc268d457051
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# Läs in en medieresurs i MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp. Detta är ett sätt att läsa in en medieresurs.

1. Ange det uppspelningsbara objektet `MediaPlayer` med den nya resurs som ska spelas upp.

   Ersätt det befintliga MediaPlayers uppspelningsbara objekt genom att anropa `MediaPlayer.replaceCurrentResource` och skicka en befintlig `MediaResource`-instans.

1. Kontrollera om det finns minst följande ändringar:

   * INITIERAD
   * FÖRBEREDD
   * FEL

      Genom dessa händelser kan `MediaPlayer`-objektet meddela programmet när mediaresursen har lästs in.

1. När mediespelarens tillstånd ändras till INITIALIZED kan du anropa `MediaPlayer.prepareToPlay`

   Initieringstillståndet anger att mediet har lästs in. Om du anropar `prepareToPlay` startar du annonsupplösningen och placeringsprocessen, om det finns någon.

1. När mediespelarens status ändras till PREPARED har medieströmmen lästs in och förbereds för uppspelning.

   När medieströmmen läses in skapas en `MediaPlayerItem`.

Om ett fel inträffar växlar MediaPlayer till FELstatus. Programmet meddelas också genom att `STATUS_CHANGED`-händelsen skickas till `MediaPlayerStatusChangeEvent`-återanropet.

Detta skickar flera parametrar:
* En `type`-parameter av typen sträng med värdet `ERROR`.

* En `MediaError`-parameter som du kan använda för att få ett meddelande som innehåller diagnostikinformation om felhändelsen.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

Följande förenklade exempelkod visar processen för inläsning av en medieresurs:

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
