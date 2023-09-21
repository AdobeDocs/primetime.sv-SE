---
description: Du kan anpassa metadata för annonsinfogning.
title: Anpassa metadata för annonsinfogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

   The `timeout` -egenskapen definieras i `AdvertisingMetadata` och den här tidsgränsen kan anges för anpassade annonsinställningar som härleds från `AdvertisingMetadata` klassen. Om användare till exempel definierar anpassade inställningar för en FreeWheel-lösare kan de ange en standardtimeout med den här inställningen.

1. Skapa `MediaPlayerItemConfig` med annonsinställningarna i steg 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Använd den här konfigurationen vid anrop `replaceCurrentResource` på `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
