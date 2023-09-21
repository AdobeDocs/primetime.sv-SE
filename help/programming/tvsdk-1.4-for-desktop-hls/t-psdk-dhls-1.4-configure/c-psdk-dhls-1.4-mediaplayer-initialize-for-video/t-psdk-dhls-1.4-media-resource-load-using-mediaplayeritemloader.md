---
description: Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.
title: Läsa in en medieresurs med MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Läsa in en medieresurs med MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.

Via `MediaPlayerItemLoader` -klassen kan du byta ut en medieresurs för motsvarande `MediaPlayerItem` utan att bifoga en vy till en `MediaPlayer` som skulle leda till att maskinvaruresurserna för videoavkodning allokeras. Processen för att få `MediaPlayerItem` -instansen är asynkron.

1. Implementera händelseavlyssnare för dessa `MediaPlayerItemLoader` händelser:

   * `MediaPlayerItemLoaderEvent.ERROR` event

     TVSDK använder detta för att informera programmet om att ett fel har inträffat. TVSDK tillhandahåller en felegenskap som innehåller diagnostikinformation.

1. Registrera den här instansen för `MediaPlayerItemLoader`.
1. Utlysning `DefaultMediaPlayerItemLoader.load`, skicka en instans av en `MediaResource` -objekt.

   URL:en för `MediaResource` -objektet måste peka på den ström som du vill få information om. Till exempel:

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
