---
description: 'TVSDK för Android innehåller en mängd olika funktioner och har följande huvudfunktioner '
title: Funktioner i Primetime TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Primetime TVSDK-funktioner{#primetime-tvsdk-features}

TVSDK för Android innehåller en mängd olika funktioner och har följande huvudfunktioner:

* VOD och live/linjär uppspelning

   * Hantering av uppspelningsfönstret, inklusive metoder för att spela upp, stoppa, pausa, söka efter och hämta spelhuvudets position
   * Stöd för repriser vid alla evenemang
   * Undertexter (608, 708, WebVTT) och alternativa former av ljud ger ökad tillgänglighet
   * Kontroll för textformat i bildtexter
   * DVR-kapacitet, snabb framåtspolning/snabb tillbakaspolning (trippelläge)
   * Logik för anpassad bithastighet (ABR) och inledande konfiguration av ABR-kontroller
   * Stöd för realtidsmanifestväxling
   * Justerbara uppspelningsbuffertar
   * Spårningssupport för fragmentets varaktighet, storlek och tid för hämtning

* Reklam

   * VPAID 2.0
   * Annonssammanfogning på klientsidan

      * Delvis annonsinfogning, som gör det möjligt för en TV-liknande upplevelse att kunna delta mitt i en annons.
      * Smidig annonsinfogning, inklusive stöd för VAST/VMAP
      * Stöd för anpassade cue-taggar för annonser
      * Stöd för markering, ersättning och borttagning av C3-annonser
      * Anpassningsbart arbetsflöde för innehåll/annonsinfogning, inklusive utpressningssignalering

* Skydd av innehåll

   * Tillgång till DRM-relaterade tjänster
   * Uppspelning av HLS-strömmar okrypterat eller med Protected HTTP Live Streaming (PHLS)
   * Upplösningsbaserad utdatakontroll, baserad på DRM-princip

* Video- och annonsspårning

   * QoS-händelsespårning
   * Meddelanden som hjälper TVSDK och ditt program att kommunicera asynkront om status för videoklipp, annonser och andra element samt om loggaktiviteten

* Loggning

   * Felsökningsloggning
   * Spårningsstöd för fragmentets varaktighet, storlek och tid för hämtning

