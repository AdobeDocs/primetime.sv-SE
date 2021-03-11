---
description: Du kan anpassa metadata för annonsinfogning.
title: Anpassa metadata för annonsinfogning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Anpassa metadata för annonsinfogning{#customize-ad-insertion-metadata}

Du kan anpassa metadata för annonsinfogning.

1. Ange en tidsgräns för annonsmetadata för olösta affärsmöjligheter.

   Standardvärdet för den här tidsgränsen är 20 sekunder.
1. Om du vill ändra värdet till 10 sekunder anger du följande:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   Egenskapen `timeout` definieras i klassen `AdvertisingMetadata` och den här tidsgränsen kan anges för anpassade annonsinställningar som härleds från klassen `AdvertisingMetadata`. Om användare till exempel definierar anpassade inställningar för en FreeWheel-lösare kan de ange en standardtimeout med den här inställningen.

1. Skapa `MediaPlayerItemConfig` med annonsinställningarna i steg 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Använd den här konfigurationen när du anropar `replaceCurrentResource` på `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

