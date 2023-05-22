---
description: Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.
title: Ställ in metadata för annonsinfogning
exl-id: da5bfdc1-2c55-45f2-b2a8-3e32450cb30d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Ställ in metadata för annonsinfogning {#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.

>[!TIP]
>
>Adobe Primetime annonsbeslut kallades tidigare Auditude.

Advertising metadata is in the `MediaResource.Metadata` -egenskap. När du startar uppspelningen av en ny video ansvarar ditt program för att ställa in rätt annonsmetadata.

1. Bygg `AuditudeSettings` -instans.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetime annonsbeslut `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>`och valfria parametrar för målinriktning.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >Medie-ID används av TVSDK som en sträng, som konverteras till ett md5-värde och används för `u` i Primetimes URL-begäran för annonsbeslut. Till exempel:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Skapa en `MediaResource` -instans genom att använda medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Läs in `MediaResource` genom `MediaPlayer.replaceCurrentResource` -metod.

   The `MediaPlayer` börjar läsa in och bearbeta medieströmmens manifest.

1. När `MediaPlayer` övergångar till INITIALIZED-status, hämta egenskaper för medieströmmen i form av en `MediaPlayerItem` via `MediaPlayer.CurrentItem` -metod.
1. (Valfritt) Fråga `MediaPlayerItem` -instans för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller om strömmen är skyddad.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Utlysning `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen är `MediaPlayer` övergångar till `PREPARED` tillstånd.
1. Utlysning `MediaPlayer.play` för att starta uppspelningen.

TVSDK inkluderar nu annonser när era medier spelas upp.
