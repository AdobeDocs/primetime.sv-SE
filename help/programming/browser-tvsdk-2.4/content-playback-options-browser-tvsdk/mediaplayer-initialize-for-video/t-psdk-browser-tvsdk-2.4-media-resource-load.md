---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.
seo-description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.
seo-title: Läsa in en medieresurs i MediaPlayer
title: Läsa in en medieresurs i MediaPlayer
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Läsa in en medieresurs i MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.

1. Ställ in `MediaPlayer` objektets uppspelningsbara objekt med den nya resurs som ska spelas upp.

   Ersätt det befintliga `MediaPlayer` objektets uppspelningsbara objekt genom att anropa `replaceCurrentResource` och skicka en befintlig `MediaResource` instans.

1. Vänta tills Browser TVSDK skickar `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status` något av följande:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Genom dessa händelser meddelar MediaPlayer-objektet programmet om medieresursen har lästs in.

1. När mediespelarens tillstånd ändras till `MediaPlayerStatus.INITIALIZED`kan du ringa `MediaPlayer.prepareToPlay`.

   Initieringstillståndet anger att mediet har lästs in. Anrop `prepareToPlay` startar upplösningen av annonsen och placeringsprocessen, om det finns någon.
1. När Browser TVSDK skickar händelsen `MediaPlayerStatus.PREPARED` har medieströmmen lästs in (ett MediaPlayerItem skapas) och förbereds för uppspelning.

Om ett fel inträffar växlar `MediaPlayer` programmet till `MediaPlayerStatus.ERROR`.

Det meddelar även programmet genom att skicka `MediaPlayerStatus.ERROR` händelsen.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


Följande förenklade exempelkod visar processen för inläsning av en medieresurs:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
