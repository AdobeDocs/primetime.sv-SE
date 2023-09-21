---
description: TVSDK för iOS innehåller en mängd olika funktioner.
title: Funktioner i Primetime TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Funktioner i Primetime TVSDK {#primetime-tvsdk-features}

TVSDK för iOS innehåller en mängd olika funktioner och har följande huvudfunktioner:

* VOD och live/linjär uppspelning

   * Hantering av uppspelningsfönstret, inklusive metoder för att spela upp, stoppa, pausa, söka efter och hämta spelhuvudets position
   * Stöd för repriser vid alla evenemang
   * Undertexter (608, WebVTT) och alternativa ljudformer ger ökad tillgänglighet
   * DVR-kapacitet
   * Logik för anpassad bithastighet (ABR) och inledande konfiguration av ABR-kontroller
   * Prenumeration på icke-HLS- och HLS-taggar
   * Stöd för realtidsmanifestväxling

* Reklam

   * VPAID 2.0
   * Annonssammanfogning på klientsidan

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
   * Integrering med Adobe Analytics och stöd för hjärtslag

* Loggning

   * Felsökningsloggning
