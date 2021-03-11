---
description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
title: Implementera snabbt framåt och bakåt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Översikt {#implement-fast-forward-and-rewind-overview}

När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill gå över till trickuppspelningsläget måste du ange ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.

Om du vill växla hastighet måste du ange ett värde.

1. Gå från normalt uppspelningsläge (1x) till trimningsläge genom att ställa in hastigheten på `MediaPlayer` till ett tillåtet värde.

   * Klassen `MediaPlayerItem` definierar tillåtna uppspelningshastigheter.
   * TVSDK väljer den närmaste tillåtna hastigheten om den angivna hastigheten inte tillåts.

   I det här exemplet ställs spelarens interna uppspelningshastighet in på den begärda hastigheten.

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. Du kan avlyssna ränteförändringshändelser, som du får veta när du har begärt en tariffändring och när en prisändring faktiskt inträffar.

       TVSDK skickar följande händelser som är relaterade till trick play:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` när  `rate` värdet ändras till ett annat värde.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` när uppspelningen återupptas med vald hastighet.

      TVSDK skickar båda dessa händelser när spelaren återgår från trippelläge till normalt uppspelningsläge.

