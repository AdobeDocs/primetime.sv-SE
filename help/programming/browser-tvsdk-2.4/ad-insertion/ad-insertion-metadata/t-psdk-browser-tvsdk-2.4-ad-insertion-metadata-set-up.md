---
description: Använd hjälpklassen AuditudeSettings för att ställa in Adobe Primetime-metadata för annonsbeslut.
title: Ställ in metadata för annonsinfogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Ställ in metadata för annonsinfogning{#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings för att ställa in Adobe Primetime-metadata för annonsbeslut.

>[!TIP]
>
>Adobe Primetime annonsbeslut kallades tidigare Auditude .

1. Bygg `AuditudeSettings` -instans.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetime annonsbeslutande mediaID, zoneID, domain och de valfria målinriktningsparametrarna.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Skapa en `MediaResource` -instans med medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Läs in `MediaResource` genom `MediaPlayer.replaceCurrentResource(resource)` -metod.

   The `MediaPlayer` börjar läsa in och bearbeta medieströmmens manifest.

1. När `MediaPlayer` övergångar till INITIALIZED-status, hämta egenskaper för medieströmmen i form av en `MediaPlayerItem` via `MediaPlayer.CurrentItem` -attribut.
1. (Valfritt) Fråga `MediaPlayerItem` -instans för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller inte.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Utlysning `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen är `  MediaPlayer ` övergångar till tillståndet PREPARED.
1. Utlysning `MediaPlayer.play` för att starta uppspelningen.
Webbläsarens TVSDK innehåller nu annonser när mediet spelas upp.
