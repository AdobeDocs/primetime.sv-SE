---
description: När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.
title: Ange en ström vid en viss tidpunkt
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Ange en ström vid en viss tidpunkt{#enter-a-stream-at-a-specific-time}

När uppspelningen startar startar VOD-media som standard vid 0, och direktmedia startar vid klientens direktpunkt (MediaPlayer.LIVE_POINT). Du kan åsidosätta standardbeteendet.

1. Skicka en position till `MediaPlayer.prepareToPlay`.
1. Webbläsarens TVSDK använder den här positionen som utgångspunkt för resursen.

   >[!NOTE]
   >
   >Ingen sökåtgärd krävs.

1. Om positionen inte ligger inom sökbart intervall används standardpositionerna.

   Till exempel:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```
