---
description: TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
title: Prenumerera på egna taggar
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Prenumerera på egna taggar{#subscribe-to-custom-tags}

TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna.
Om du vill prenumerera på taggar tilldelar du en vektor som innehåller de anpassade taggnamnen till `subscribedTags` -egenskap. Om du även behöver ändra de annonstaggar som används av standardgeneratorn för affärsmöjlighet tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` -egenskap.

För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange egna annonstaggnamn globalt genom att tilldela en vektor som innehåller de anpassade taggarna till `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Du måste inkludera `#` prefix när du arbetar med HLS-strömmar.

   Till exempel:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Om du vill ändra annonstaggarna som används av standardgeneratorn för affärsmöjlighet globalt tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` egenskap i `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Ersätt den aktuella resursen om du vill att alla globala inställningar ska gälla.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Så här anger du prenumererade taggnamn för en ström, om det behövs:
   1. Skapa en mediespelarobjektskonfiguration.

      >[!TIP]
      >
      >Det enklaste sättet är att skapa en standardkonfiguration för mediaspelarobjekt.

   1. Tilldela en vektor som innehåller de anpassade taggarna till `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Om du vill ändra de annonstaggar som används av standardgeneratorn för affärsmöjlighet i den angivna strömmen tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` egenskap i `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Om du vill att ändringarna för strömmen ska börja gälla när du läser in medieströmmen använder du objektkonfigurationen för mediaspelaren.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
