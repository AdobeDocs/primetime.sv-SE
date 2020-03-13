---
description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
seo-description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
seo-title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
uuid: cf973caf-be29-46ce-bfa4-651e7653f8d4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar.

Du kan ange att TVSDK ska flytta spelhuvudet till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Konfigurera en metadatainstans med `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` uppräkningen inställd på strängvärdet &quot;true&quot; (inte som Boolean `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Skapa och konfigurera en `MediaResource` instans och skicka ytterligare konfigurationsalternativ till `TimeRangeCollection.toMetadata`. Den här metoden tar emot ytterligare konfigurationsalternativ via en annan generisk metadatastruktur.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

