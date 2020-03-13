---
description: Använd hjälpklassen AuditudeSettings för att ställa in metadata för Adobe Primetime-annonsering.
seo-description: Använd hjälpklassen AuditudeSettings för att ställa in metadata för Adobe Primetime-annonsering.
seo-title: Ställ in metadata för annonsinfogning
title: Ställ in metadata för annonsinfogning
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Ställ in metadata för annonsinfogning{#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings för att ställa in metadata för Adobe Primetime-annonsering.

>[!TIP]
>
>Adobe Primetimes annonsbeslut hette tidigare Auditude.

1. Bygg `AuditudeSettings` instansen.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetimes annonsbeslutande mediaID, zoneID, domain och de valfria målinriktningsparametrarna.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Skapa en `MediaResource` instans med hjälp av medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Läs in `MediaResource` objektet via `MediaPlayer.replaceCurrentResource(resource)` metoden.

   Inläsningen och bearbetningen av medieströmmens manifest `MediaPlayer` påbörjas.

1. När du övergår till `MediaPlayer` INITIALIZED-status hämtar du medieströmsegenskaperna i form av en `MediaPlayerItem` instans via `MediaPlayer.CurrentItem` attributet.
1. (Valfritt) Fråga `MediaPlayerItem` instansen för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller inte.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Ring `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen övergår `  MediaPlayer ` de till tillståndet PREPARED.
1. Anropa `MediaPlayer.play` för att starta uppspelningen.
Webbläsarens TVSDK innehåller nu annonser när mediet spelas upp.
