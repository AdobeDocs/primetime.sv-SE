---
description: Använd hjälpklassen AuditudeSettings för att ställa in Adobe Primetime-metadata för annonsbeslut.
seo-description: Använd hjälpklassen AuditudeSettings för att ställa in Adobe Primetime-metadata för annonsbeslut.
seo-title: Ställ in metadata för annonsinfogning
title: Ställ in metadata för annonsinfogning
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Ställ in metadata för annonsinfogning{#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings för att ställa in Adobe Primetime-metadata för annonsbeslut.

>[!TIP]
>
>Adobe Primetime annonsbeslut kallades tidigare Auditude.

1. Bygg `AuditudeSettings`-instansen.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetime annonsbeslutande mediaID, zoneID, domain och de valfria målinriktningsparametrarna.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Skapa en `MediaResource`-instans med hjälp av medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Läs in `MediaResource`-objektet via metoden `MediaPlayer.replaceCurrentResource(resource)`.

   `MediaPlayer` börjar läsa in och bearbeta medieströmmens manifest.

1. När `MediaPlayer` övergår till INITIALIZED-status hämtar du medieströmsegenskaperna i form av en `MediaPlayerItem`-instans via `MediaPlayer.CurrentItem`-attributet.
1. (Valfritt) Fråga `MediaPlayerItem`-instansen för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller inte.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Ring `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen övergår `  MediaPlayer ` till tillståndet PREPARED.
1. Starta uppspelningen genom att anropa `MediaPlayer.play`.
Webbläsarens TVSDK innehåller nu annonser när mediet spelas upp.
