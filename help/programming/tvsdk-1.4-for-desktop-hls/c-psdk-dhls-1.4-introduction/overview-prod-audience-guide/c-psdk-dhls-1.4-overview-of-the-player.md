---
description: TVSDK for Desktop HLS innehåller en mängd olika funktioner och har följande huvudfunktioner
title: Funktioner i Primetime TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Funktioner i Primetime TVSDK{#primetime-tvsdk-features}

TVSDK for Desktop HLS innehåller en mängd olika funktioner och har följande huvudfunktioner:

* VOD och live/linjär uppspelning

   * Hantering av uppspelningsfönstret, inklusive metoder för att spela upp, stoppa, pausa, söka efter och hämta spelhuvudets position.
   * Undertexter (608, 708, WebVTT) och alternativa former av ljud ger ökad tillgänglighet
   * Kontroll för textformat i bildtexter
   * DVR-kapacitet, snabb framåtspolning/snabb tillbakaspolning (trippelläge)
   * Tricks play för både live- och VOD-innehåll
   * Logik för anpassad bithastighet (ABR) och inledande konfiguration av ABR-kontroller
   * Stöd för realtidsmanifestväxling
   * Justerbara uppspelningsbuffertar
   * 302 omdirigeringsoptimering
   * Spårningssupport för fragmentets varaktighet, storlek och tid för hämtning

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
   * Stöd för cookies och cookies för medieautentisering
   * Paketering av token i flera domäner

* Video- och annonsspårning

   * QoS-händelsespårning
   * Meddelanden som hjälper TVSDK och ditt program att kommunicera asynkront om status för videoklipp, annonser och andra element samt om loggaktiviteten.
   * Integrering med Adobe Analytics och stöd för hjärtslag

* Loggning

   * Felsökningsloggning.
   * Spårningsstöd för fragmentvaraktighet, storlek och nedladdningstid.
