---
description: Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.
seo-description: Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.
seo-title: Ställ in metadata för annonsinfogning
title: Ställ in metadata för annonsinfogning
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Ställ in metadata för annonsinfogning {#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.

>[!TIP]
>
>Adobe Primetime annonsbeslut kallades tidigare Auditude.

Advertising metadata finns i egenskapen `MediaResource.Metadata`. När du startar uppspelningen av en ny video ansvarar ditt program för att ställa in rätt annonsmetadata.

1. Bygg `AuditudeSettings`-instansen.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetime annonsbeslut `mediaID`, `zoneID`, `domain` och de valfria målinriktningsparametrarna.

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
   >Medie-ID används av TVSDK som en sträng, som konverteras till ett md5-värde, och används för `u`-värdet i Primetimes URL-begäran om annonsbeslut. Exempel:
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. Skapa en `MediaResource`-instans med hjälp av medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Läs in `MediaResource`-objektet via metoden `MediaPlayer.replaceCurrentResource`.

   `MediaPlayer` börjar läsa in och bearbeta medieströmmens manifest.

1. När `MediaPlayer` övergår till `INITIALIZED`-status hämtar du medieströmsegenskaperna i form av en `MediaPlayerItem`-instans via metoden `MediaPlayer.CurrentItem`.
1. (Valfritt) Fråga `MediaPlayerItem`-instansen för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller om strömmen är skyddad.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Ring `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen övergår `MediaPlayer` till läget `PREPARED`.
1. Starta uppspelningen genom att anropa `MediaPlayer.play`.

TVSDK inkluderar nu annonser när era medier spelas upp.
