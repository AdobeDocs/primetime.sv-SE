---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-title: Ange en ström vid en viss tidpunkt
title: Ange en ström vid en viss tidpunkt
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Ange en ström vid en viss tidpunkt {#enter-a-stream-at-a-specific-time}

Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.

1. Skicka en position till `MediaPlayer.prepareToPlay`.

   TVSDK anser att den angivna positionen är utgångspunkten för tillgången och ingen sökåtgärd krävs. Om positionen inte ligger inom det sökbara intervallet använder TVSDK standardpositionen. Mer information finns i [Läsa in en medieresurs i mediespelaren](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

   Exempel:

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
