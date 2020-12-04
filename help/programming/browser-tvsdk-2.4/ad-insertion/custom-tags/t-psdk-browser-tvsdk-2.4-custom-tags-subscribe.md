---
description: Browser TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i MPD-filen (Media Presentation Description).
seo-description: Browser TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i MPD-filen (Media Presentation Description).
seo-title: Prenumerera på anpassade annonstaggar
title: Prenumerera på anpassade annonstaggar
uuid: 208f61f4-dc33-4363-aa71-878458740a8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Prenumerera på anpassade annonstaggar{#subscribe-to-custom-ad-tags}

Browser TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i MPD-filen (Media Presentation Description).

Du måste prenumerera på taggarna innan uppspelningen startar.
Om du vill prenumerera på taggar anger du en vektor som innehåller de anpassade taggnamnen till egenskapen `subscribedTags`. Om du även behöver ändra de annonstaggar som används av standardgeneratorn för affärsmöjlighet anger du en vektor som innehåller de anpassade annonstaggnamnen till egenskapen `adTags`.

Så här prenumererar du på anpassade taggar:

1. Skapa en ny konfiguration för mediespelarobjekt.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Skapa en tom strängvektor.

   ```js
   var subscribeTags = [];
   ```

1. Lägg till egna taggnamn i den här vektorn.

   >[!IMPORTANT]
   >
   >Om du har att göra med HLS-strömmar måste du komma ihåg att ta med prefixet `#`.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Tilldela den uppdaterade vektorn till egenskapen `mediaPlayerItemConfig.subscribeTags`.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Skapa en tom strängvektor.

   ```js
   var adTags= [];
   ```

1. Lägg till det anpassade annonstaggnamnet i den här vektorn.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Tilldela den uppdaterade vektorn till egenskapen `mediaPlayerItemConfig.adTags`.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Använd mediespelarobjektets konfiguration när du läser in medieströmmen.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

