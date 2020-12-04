---
description: Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.
seo-description: Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.
seo-title: Läsa in en medieresurs med MediaPlayerItemLoader
title: Läsa in en medieresurs med MediaPlayerItemLoader
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Läsa in en medieresurs med MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Ett annat sätt att lösa en medieresurs är med MediaPlayerItemLoader. Detta är användbart när du vill få information om en viss medieström utan att initiera en MediaPlayer-instans.

Genom klassen `MediaPlayerItemLoader` kan du byta ut en medieresurs för motsvarande `MediaPlayerItem` utan att bifoga en vy till en `MediaPlayer`-instans, vilket skulle leda till allokering av maskinvaruresurser för videoavkodning. Processen att hämta `MediaPlayerItem`-instansen är asynkron.

1. Implementera `MediaPlayerItemLoader.LoaderListener`-återanropsgränssnittet.

       Gränssnittet definierar två metoder:
   
   * `LoaderListener.onError` callback-funktion

      TVSDK använder detta för att informera programmet om att ett fel har inträffat. TVSDK tillhandahåller en felkod som parametrar och en beskrivningssträng som innehåller diagnostikinformation.

   * `LoaderListener.onError` callback-funktion

      TVSDK använder detta för att informera programmet om att den begärda informationen finns tillgänglig i form av en `MediaPlayerItem`-instans som skickas som en parameter till återanropet.

1. Registrera den här instansen hos TVSDK genom att skicka den som en parameter till konstruktorn för `MediaPlayerItemLoader`.
1. Anropa `MediaPlayerItemLoader.load` och skicka en instans av ett `MediaResource`-objekt.

   URL:en för `MediaResource`-objektet måste peka på den ström som du vill få information om. Exempel:

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

