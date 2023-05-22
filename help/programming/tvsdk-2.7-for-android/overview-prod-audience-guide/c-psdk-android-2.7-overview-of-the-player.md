---
description: TVSDK för Android 2.5 innehåller en mängd funktioner som du kan implementera i dina spelare.
title: Funktioner i Primetime TVSDK
exl-id: 1f1ea807-67b0-4dfa-adf3-198207f57aff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Funktioner i Primetime TVSDK {#primetime-tvsdk-features}

TVSDK för Android 2.7 innehåller en mängd funktioner som du kan implementera i dina spelare.

TVSDK-funktioner:

* **VOD och live/linjär uppspelning**

   * Hantering av uppspelningsfönstret, inklusive metoder för att spela upp, stoppa, pausa, söka efter och hämta spelhuvudets position
   * Stöd för repriser vid alla evenemang
   * Undertexter (608, 708, WebVTT) och alternativa former av ljud ger ökad tillgänglighet
   * Kontroller för textformat i bildtexter
   * DVR-kapacitet, snabb framåtspolning och snabb tillbakaspolning (de två senare kallas för *tricks-play-läge*)
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
