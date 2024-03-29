---
description: Följ de här stegen för att skapa en grundläggande spelare med webbläsarens TVSDK.
title: Skapa en basspelare med TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Skapa en basspelare med TVSDK{#create-a-basic-player-using-tvsdk}

Följ de här stegen för att skapa en grundläggande spelare med webbläsarens TVSDK.

1. Skapa en ny katalog där du kan hämta komprimerade filer för Browser TVSDK.
1. Ladda ned Browser TVSDK från Zendesk, expandera filerna och placera ramverksmappen i den nya katalogen.
1. Skapa en enkel HTML-mallsida för koden med en `div` i den.
1. Placera den här mallsidan i en HTML-fil i den katalog som du skapade i steg 1.

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. Lägg till Browser TVSDK-biblioteken i head-avsnittet.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. För body-taggen lägger du till `onLoad` -avsnitt.

   ```
   <body onload="startVideo()">
   ```

1. Börja implementera `startVideo` funktion.
1. Lägga till en script-tagg och skapa `startVideo` -funktionen i -taggen.

   Det här ska finnas i sidans head-avsnitt.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Skapa `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Skapa `MediaPlayerView`.

   >[!TIP]
   >
   >Det är här `div` som du skapade tidigare används.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Lägg till händelseavlyssnaren för spelaren.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementera händelsehanteraren och placera den före händelseavlyssnaren add.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. Skapa `MediaResource`, som skickar M3U8-länken (eller mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Skapa en tom konfiguration och ersätt resursen.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. När spelaren är i INITIALIZED-läge ska du ringa `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. När spelaren är i tillståndet PREPARED ringer du `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
