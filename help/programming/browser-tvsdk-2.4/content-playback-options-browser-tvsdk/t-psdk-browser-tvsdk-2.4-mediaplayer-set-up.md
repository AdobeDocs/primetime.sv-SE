---
description: Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.
seo-description: Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.
seo-title: Konfigurera MediaPlayer
title: Konfigurera MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Konfigurera MediaPlayer{#set-up-the-mediaplayer}

Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.

1. Skapa en `MediaPlayer`-instans med följande:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Skapa en `MediaPlayerView`-instans:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   där `container` är målelementet `div` som innehåller din `HTMLMediaElement`.

   På en HTML-sida:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Utlysning:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Koppla din `MediaPlayerView`-instans till din `MediaPlayer`-instans:

   ```js
   player.view = view;
   ```

1. Koppla det anpassade kontrollelementet `div` till din MediaPlayer-instans.

   I HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Utlysning:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

Instansen `MediaPlayer` är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.
