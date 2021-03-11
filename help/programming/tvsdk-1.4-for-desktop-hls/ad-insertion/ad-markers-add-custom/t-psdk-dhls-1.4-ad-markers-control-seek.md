---
description: Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.
title: Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Styra uppspelningsbeteendet för sökning efter anpassade annonsmarkörer{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Du kan åsidosätta standardbeteendet för hur TVSDK söker efter annonser när du använder anpassade annonsmarkörer.

Som standard hoppas annonserna över av TVSDK när en användare söker i eller förbi annonsavsnitt som är ett resultat av placeringen av anpassade annonsmärken. Detta kan skilja sig från det aktuella uppspelningsbeteendet för standardannonsbrytningar.

Du kan ange att TVSDK ska flytta spelhuvudet till början av den senast hoppade anpassade annonsen när användaren söker efter en eller flera anpassade annonser.

1. Konfigurera en metadatainstans med uppräkningen `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` inställd på strängvärdet &quot;true&quot; (inte som ett booleskt `true`).

1. Skapa och konfigurera en `MediaResource`-instans och skicka de extra konfigurationsalternativen till `TimeRangeCollection.toMetadata`. Den här metoden tar emot ytterligare konfigurationsalternativ via en annan generisk metadatastruktur.

