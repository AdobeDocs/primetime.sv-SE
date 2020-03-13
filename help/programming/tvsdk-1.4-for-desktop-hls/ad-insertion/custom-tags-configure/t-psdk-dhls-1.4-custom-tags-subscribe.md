---
description: TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-description: TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.
seo-title: Prenumerera på egna taggar
title: Prenumerera på egna taggar
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Prenumerera på egna taggar{#subscribe-to-custom-tags}

TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i innehållsmanifestet.

Innan uppspelningen startar måste du prenumerera på taggarna.
Om du vill prenumerera på taggar tilldelar du en vektor som innehåller de anpassade taggnamnen till `subscribedTags` egenskapen. Om du även behöver ändra de annonstaggar som används av standardgeneratorn för affärsmöjlighet tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` egenskapen.

För att få meddelanden om anpassade taggar i HLS-manifestationer:

1. Ange egna annonstaggnamn globalt genom att tilldela en vektor som innehåller de anpassade taggarna `subscribeTags` i `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Du måste ta med prefixet `#` när du arbetar med HLS-strömmar.

   Exempel:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Om du vill ändra annonstaggarna som används av standardgeneratorn för affärsmöjlighet globalt, tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` egenskapen i `PSDKConfig`.

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

   1. Tilldela en vektor som innehåller de anpassade taggar som ska `subscribeTags` användas `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Om du vill ändra de annonstaggar som används av standardgeneratorn för affärsmöjlighet i den angivna strömmen tilldelar du en vektor som innehåller de anpassade annonstaggnamnen till `adTags` egenskapen i `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Om du vill att ändringarna för strömmen ska börja gälla när du läser in medieströmmen använder du objektkonfigurationen för mediaspelaren.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

