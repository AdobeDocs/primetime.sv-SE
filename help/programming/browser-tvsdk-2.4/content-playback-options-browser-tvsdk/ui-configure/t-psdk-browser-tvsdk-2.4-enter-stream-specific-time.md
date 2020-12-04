---
description: När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-description: När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
seo-title: Ange en ström vid en viss tidpunkt
title: Ange en ström vid en viss tidpunkt
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# Ange en ström vid en viss tidpunkt{#enter-a-stream-at-a-specific-time}

När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.

1. Skicka en position till `MediaPlayer.prepareToPlay`.
1. Webbläsarens TVSDK använder den här positionen som utgångspunkt för resursen.

   >[!NOTE]
   >
   >Ingen sökåtgärd krävs.

1. Om positionen inte ligger inom sökbart intervall används standardpositionerna.

   Exempel:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

