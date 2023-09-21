---
description: Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.
title: Läsa in en medieresurs i MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Läsa in en medieresurs i MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Läs in en resurs genom att direkt instansiera en MediaResource och läsa in det videoinnehåll som ska spelas upp.

1. Ställ in `MediaPlayer` objektets uppspelningsbara objekt med den nya resurs som ska spelas upp.

   Ersätt din befintliga `MediaPlayer` objektets uppspelningsbara objekt genom att anropa `replaceCurrentResource` och skicka en befintlig `MediaResource` -instans.

1. Vänta på att webbläsarens TVSDK ska skicka `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status` som är lika med något av följande:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

     Genom dessa händelser meddelar MediaPlayer-objektet programmet om medieresursen har lästs in.

1. När mediespelarens tillstånd ändras till `MediaPlayerStatus.INITIALIZED`kan du ringa `MediaPlayer.prepareToPlay`.

   INITIALIZED-läget anger att mediet har lästs in. Anropar `prepareToPlay` startar processen för upplösning och placering av annonser, om sådan finns.
1. När webbläsarens TVSDK skickar `MediaPlayerStatus.PREPARED` händelsen när medieströmmen har lästs in (ett MediaPlayerItem skapas) och förbereds för uppspelning.

Om ett fel uppstår visas `MediaPlayer` växlar till `MediaPlayerStatus.ERROR`.

Programmet meddelas också genom att `MediaPlayerStatus.ERROR` -händelse.

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
