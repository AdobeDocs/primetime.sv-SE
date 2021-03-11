---
description: När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
title: Ange en ström vid en viss tidpunkt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
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

