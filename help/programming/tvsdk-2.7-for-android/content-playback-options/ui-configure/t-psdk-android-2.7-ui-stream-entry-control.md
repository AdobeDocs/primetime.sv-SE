---
description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-description: Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-title: Ange en ström vid en viss tidpunkt
title: Ange en ström vid en viss tidpunkt
uuid: 65a19192-b890-4d69-9cb1-582a22988d2b
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# Ange en ström vid en viss tidpunkt {#enter-a-stream-at-a-specific-time}

Som standard startar VOD-media vid uppspelning vid 0 och direktmedia vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.

1. Skicka en position till `MediaPlayer.prepareToPlay`.

   TVSDK anser att den angivna positionen är utgångspunkten för tillgången och ingen sökåtgärd krävs. Om positionen inte ligger inom det sökbara intervallet använder TVSDK standardpositionen. Mer information finns i [Läs in en medieresurs i mediespelaren](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

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

