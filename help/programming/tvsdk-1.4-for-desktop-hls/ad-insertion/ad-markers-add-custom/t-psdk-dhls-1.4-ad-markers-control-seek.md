---
description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
exl-id: c821e0be-1490-4b5f-8f9f-bffdfb1a982d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar.

Du kan ange att TVSDK ska flytta spelhuvudet till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Konfigurera en metadatainstans med `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` uppräkning inställd på strängvärdet &quot;true&quot; (inte som Boolean `true`).

1. Skapa och konfigurera en `MediaResource` -instans, skicka ytterligare konfigurationsalternativ till `TimeRangeCollection.toMetadata`. Den här metoden tar emot ytterligare konfigurationsalternativ via en annan generisk metadatastruktur.
