---
description: TVSDK för Android 3.4 innehåller en mängd funktioner som du kan implementera i dina spelare.
seo-description: TVSDK för Android 3.4 innehåller en mängd funktioner som du kan implementera i dina spelare.
seo-title: Funktioner i Primetime TVSDK
title: Funktioner i Primetime TVSDK
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Primetime TVSDK-funktioner {#primetime-tvsdk-features}

TVSDK för Android 3.9 innehåller en mängd funktioner som du kan implementera i dina spelare.

TVSDK-funktioner:

* **VOD och live/linjär uppspelning**

   * Hantering av uppspelningsfönstret, inklusive metoder för att spela upp, stoppa, pausa, söka efter och hämta spelhuvudets position
   * Stöd för repriser vid alla evenemang
   * Undertexter (608, 708, WebVTT) och alternativa former av ljud ger ökad tillgänglighet
   * Kontroller för textformat i bildtexter
   * DVR-kapacitet, snabb framåtspolning och snabb tillbakaspolning (de två senare kallas *tricks-play-läge*)
   * Logik för anpassad bithastighet (ABR) och inledande konfiguration av ABR-kontroller
   * Stöd för realtidsmanifestväxling
   * Justerbara uppspelningsbuffertar
   * Spårningssupport för fragmentets varaktighet, storlek och tid för hämtning

* **Reklam**

   * VPAID 2.0
   * Annonssammanfogning på klientsidan

      * Smidig annonsinfogning, inklusive stöd för VAST/VMAP
      * Stöd för anpassade cue-taggar för annonser
      * Stöd för markering, ersättning och borttagning av C3-annonser
      * Anpassningsbart arbetsflöde för innehåll/annonsinfogning, inklusive utpressningssignalering

* **Skydd av innehåll**

   * Tillgång till DRM-relaterade tjänster
   * Uppspelning av HLS-strömmar okrypterat eller med Protected HTTP Live Streaming (PHLS)
   * Upplösningsbaserad utdatakontroll, baserad på DRM-princip

* **Video- och annonsspårning**

   * QoS-händelsespårning
   * Meddelanden som hjälper TVSDK och ditt program att kommunicera asynkront om status för videoklipp, annonser och andra element. Meddelanden loggar även aktivitet.

* **Loggning**

   * Felsökningsloggning
   * Spårningsstöd för fragmentvaraktighet, storlek och nedladdningstid.

* **Säker leverans**

   * Stöd för säker leverans (HTTPS) för alla anrop från TVSDK.