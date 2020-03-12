---
description: Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in metadata för Adobe Primetime-annonsbeslut.
seo-description: Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in metadata för Adobe Primetime-annonsbeslut.
seo-title: Ställ in metadata för annonsinfogning
title: Ställ in metadata för annonsinfogning
uuid: 7400813c-6af0-4c96-a6c7-d9ea1ba6a7b9
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Ställ in metadata för annonsinfogning {#set-up-ad-insertion-metadata}

Använd hjälpklassen `AuditudeSettings`, som utökar `MetadataNode` klassen, för att ställa in metadata för Adobe Primetime-annonsering.

>[!TIP]
>
>Adobe Primetimes annonsbeslut kallades tidigare Auditude.

Advertising metadata is in the `MediaResource.Metadata` property. När du startar uppspelningen av en ny video ansvarar ditt program för att ställa in rätt annonsmetadata.

1. Bygg `AuditudeSettings` instansen.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange annonsbeslut `mediaID`, `zoneID``<ph conkeyref="phrases/primetime-sdk-name"/>`och valfria parametrar för målinriktning i Adobe Primetime.

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
   >Medie-ID används av TVSDK som en sträng, som konverteras till ett md5-värde, och används för `u` värdet i Primetimes URL-begäran om annonsbeslut. Exempel:
   >
   >`https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Skapa en `MediaResource` instans med hjälp av medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Läs in `MediaResource` objektet via `MediaPlayer.replaceCurrentResource` metoden.

   Inläsningen och bearbetningen av medieströmmens manifest `MediaPlayer` påbörjas.

1. När du övergår till `MediaPlayer` INITIALIZED-status hämtar du medieströmsegenskaperna i form av en `MediaPlayerItem` instans via `MediaPlayer.CurrentItem` metoden.
1. (Valfritt) Fråga `MediaPlayerItem` instansen för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller om strömmen är skyddad.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Ring `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen övergår de till `MediaPlayer` `PREPARED` läge.
1. Anropa `MediaPlayer.play` för att starta uppspelningen.
TVSDK inkluderar nu annonser när era medier spelas upp.
