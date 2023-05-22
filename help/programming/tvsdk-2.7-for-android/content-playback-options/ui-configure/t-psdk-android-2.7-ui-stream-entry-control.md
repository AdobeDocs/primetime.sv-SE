---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
title: Ange en ström vid en viss tidpunkt
exl-id: 2914d837-c773-42db-b744-42793e80cb95
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Ange en ström vid en viss tidpunkt {#enter-a-stream-at-a-specific-time}

Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.

1. Skicka en position till `MediaPlayer.prepareToPlay`.

   TVSDK anser att den angivna positionen är utgångspunkten för tillgången och ingen sökåtgärd krävs. Om positionen inte ligger inom det sökbara intervallet använder TVSDK standardpositionen. Mer information finns i [Läsa in en medieresurs i mediespelaren](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

   Till exempel:

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
