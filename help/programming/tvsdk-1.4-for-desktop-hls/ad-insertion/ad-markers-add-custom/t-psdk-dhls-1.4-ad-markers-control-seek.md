---
description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
seo-description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
seo-title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar.

Du kan ange att TVSDK ska flytta spelhuvudet till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Konfigurera en metadatainstans med `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` uppräkningen inställd på strängvärdet &quot;true&quot; (inte som Boolean `true`).

1. Skapa och konfigurera en `MediaResource` instans och skicka ytterligare konfigurationsalternativ till `TimeRangeCollection.toMetadata`. Den här metoden tar emot ytterligare konfigurationsalternativ via en annan generisk metadatastruktur.

