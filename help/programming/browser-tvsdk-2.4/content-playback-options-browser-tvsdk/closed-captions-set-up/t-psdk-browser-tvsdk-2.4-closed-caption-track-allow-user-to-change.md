---
description: Här är ett exempel på hur en användare kan välja ett textningsspår.
title: Tillåt användaren att ändra spåret
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# Tillåt användaren att ändra spåret{#allow-the-user-to-change-the-track}

Här är ett exempel på hur en användare kan välja ett textningsspår.

1. Om du vill visa tillgängliga spår för undertexter använder du egenskapen `MediaPlayerItem.closedCaptionsTracks`.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Om du vill ange vilket spår för undertextning som är aktuellt använder du metoden `MediaPlayerItem.selectClosedCaptionsTrack`.
1. När mediespelarobjektet har förberetts hämtar du det från mediespelaren med metoden ` MediaPlayer.  currentItem `.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

