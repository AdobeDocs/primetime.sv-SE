---
description: Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.
title: Konfigurera MediaPlayer
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Konfigurera MediaPlayer{#set-up-the-mediaplayer}

Ett MediaPlayer-objekt kapslar in en mediespelares beteende och funktioner.

1. Instansiera en `MediaPlayer` med följande:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Skapa en `MediaPlayerView` instans:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   där `container` är målet `div` element som innehåller `HTMLMediaElement`.

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

1. Bifoga dina `MediaPlayerView` instansen till `MediaPlayer` instans:

   ```js
   player.view = view;
   ```

1. Koppla de anpassade kontrollerna `div` -element till din MediaPlayer-instans.

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

The `MediaPlayer` -instansen är nu tillgänglig och korrekt konfigurerad för att visa videoinnehåll på enhetsskärmen.
