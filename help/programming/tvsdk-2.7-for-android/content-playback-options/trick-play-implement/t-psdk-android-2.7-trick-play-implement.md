---
description: När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill aktivera trickuppspelningsläget anger du ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.
title: Implementera snabbt framåt och bakåt
exl-id: 569fe22c-b1d8-46db-ab29-a50652413072
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Översikt {#implement-fast-forward-and-rewind-overview}

När användarna snabbt spolar framåt eller bakåt genom mediet är de i trickläget. Om du vill aktivera trickuppspelningsläget anger du ett annat värde än 1 för MediaPlayer-uppspelningshastigheten.

Om du vill växla hastighet måste du ange ett värde.

1. Gå från normalt uppspelningsläge (1x) till uppspelningsläge genom att ställa in hastigheten på `MediaPlayer` till ett tillåtet värde.

       Kom ihåg följande information:
   
   * The `MediaPlayerItem` -klassen definierar de tillåtna uppspelningshastigheterna.
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
