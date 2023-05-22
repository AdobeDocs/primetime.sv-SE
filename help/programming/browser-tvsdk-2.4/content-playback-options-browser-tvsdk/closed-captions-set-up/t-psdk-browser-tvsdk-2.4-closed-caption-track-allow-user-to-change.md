---
description: Här är ett exempel på hur en användare kan välja ett textningsspår.
title: Tillåt användaren att ändra spåret
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# Tillåt användaren att ändra spåret{#allow-the-user-to-change-the-track}

Här är ett exempel på hur en användare kan välja ett textningsspår.

1. Om du vill visa tillgängliga spår för undertexter använder du `MediaPlayerItem.closedCaptionsTracks` -egenskap.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Om du vill ange vilket spår för undertextning som är aktuellt använder du `MediaPlayerItem.selectClosedCaptionsTrack` -metod.
1. När mediespelarobjektet har förberetts hämtar du det från mediespelaren med hjälp av ` MediaPlayer.  currentItem ` -metod.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
