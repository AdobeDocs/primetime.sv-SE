---
description: Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.
title: Konfigurera MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
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
