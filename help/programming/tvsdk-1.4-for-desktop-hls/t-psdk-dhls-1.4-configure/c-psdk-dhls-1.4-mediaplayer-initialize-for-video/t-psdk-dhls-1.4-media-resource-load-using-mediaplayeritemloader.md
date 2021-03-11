---
description: Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.
title: Läsa in en medieresurs med MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Läsa in en medieresurs med MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.

Genom klassen `MediaPlayerItemLoader` kan du byta ut en medieresurs för motsvarande `MediaPlayerItem` utan att bifoga en vy till en `MediaPlayer`-instans, vilket skulle leda till allokering av maskinvaruresurser för videoavkodning. Processen att hämta `MediaPlayerItem`-instansen är asynkron.

1. Implementera händelseavlyssnare för dessa `MediaPlayerItemLoader`-händelser:

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK använder detta för att informera programmet om att ett fel har inträffat. TVSDK tillhandahåller en felegenskap som innehåller diagnostikinformation.

1. Registrera den här instansen hos `MediaPlayerItemLoader`.
1. Anropa `DefaultMediaPlayerItemLoader.load` och skicka en instans av ett `MediaResource`-objekt.

   URL:en för `MediaResource`-objektet måste peka på den ström som du vill få information om. Exempel:

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

