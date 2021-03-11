---
description: Browser TVSDK förbereder TimedMetadata-objekt för prenumerationstaggar varje gång dessa objekt påträffas i MPD-filen (Media Presentation Description).
title: Prenumerera på anpassade annonstaggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
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

