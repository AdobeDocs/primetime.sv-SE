---
description: Här är ett exempel på hur en användare kan välja ett textningsspår.
seo-description: Här är ett exempel på hur en användare kan välja ett textningsspår.
seo-title: Tillåt användaren att ändra spåret
title: Tillåt användaren att ändra spåret
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Tillåt användaren att ändra spåret{#allow-the-user-to-change-the-track}

Här är ett exempel på hur en användare kan välja ett textningsspår.

1. Om du vill visa tillgängliga spår för undertexter använder du `MediaPlayerItem.closedCaptionsTracks` egenskapen.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Använd `MediaPlayerItem.selectClosedCaptionsTrack` metoden för att ange vilket spår för undertextning som är aktuellt.
1. När mediespelarobjektet har förberetts hämtar du det från mediespelaren med ` MediaPlayer.  currentItem ` metoden .

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

