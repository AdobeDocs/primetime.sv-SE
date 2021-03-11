---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.
title: Läsa in en medieresurs i MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Läs in en medieresurs i MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.

1. Ange det uppspelningsbara objektet `MediaPlayer` med den nya resurs som ska spelas upp.

   Ersätt det befintliga `MediaPlayer`-objektets uppspelningsbara objekt genom att anropa `replaceCurrentResource` och skicka en befintlig `MediaResource`-instans.

1. Vänta tills Browser TVSDK skickar `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status` som är lika med något av följande:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Genom dessa händelser meddelar MediaPlayer-objektet programmet om medieresursen har lästs in.

1. När mediespelarens tillstånd ändras till `MediaPlayerStatus.INITIALIZED` kan du anropa `MediaPlayer.prepareToPlay`.

   Initieringstillståndet anger att mediet har lästs in. Om du anropar `prepareToPlay` startar du annonsupplösningen och placeringsprocessen, om det finns någon.
1. När Browser TVSDK skickar händelsen `MediaPlayerStatus.PREPARED` har medieströmmen lästs in (ett MediaPlayerItem skapas) och förbereds för uppspelning.

Om ett fel uppstår växlar `MediaPlayer` till `MediaPlayerStatus.ERROR`.

Programmet meddelas också genom att händelsen `MediaPlayerStatus.ERROR` skickas.

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
