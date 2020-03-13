---
description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill aktivera trickuppspelningsläget anger du ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
seo-description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill aktivera trickuppspelningsläget anger du ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
seo-title: Implementera snabbt framåt och bakåt
title: Implementera snabbt framåt och bakåt
uuid: 070a3331-43a3-4517-9cd9-06d817ffcfbd
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Översikt {#implement-fast-forward-and-rewind-overview}

När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill aktivera trickuppspelningsläget anger du ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.

Om du vill växla hastighet måste du ange ett värde.

1. Gå från normalt uppspelningsläge (1x) till trimningsläge genom att ställa in hastigheten på `MediaPlayer` till ett tillåtet värde.

       Kom ihåg följande information:
   
   * Klassen definierar `MediaPlayerItem` tillåtna uppspelningshastigheter.
   * TVSDK väljer den närmaste tillåtna hastigheten om den angivna hastigheten inte tillåts.

      I följande exempel ställs spelarens interna uppspelningshastighet in på den begärda hastigheten:

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. Du kan avlyssna ränteförändringshändelser, som meddelar dig när du har begärt en tariffändring och när prisförändringen faktiskt inträffar.

       TVSDK skickar följande händelser som är relaterade till trick play:
   
   * `MediaPlayerEvent.RATE_SELECTED`, när `rate` värdet ändras till ett annat värde.

   * `MediaPlayerEvent.RATE_PLAYING`när uppspelningen återupptas med vald hastighet.

      TVSDK skickar de här händelserna när spelaren återgår från tricks-uppspelningsläge till normalt uppspelningsläge.

