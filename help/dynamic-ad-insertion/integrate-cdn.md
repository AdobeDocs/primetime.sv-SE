---
title: Integrera ditt CDN
description: Integrera ditt CDN
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Integrera ditt CDN {#integrating-cdn}

Primetime Ad Insertion fungerar som en proxy mellan klientprogrammet och -manifestationerna, inte själva videosegmenten. Distribuera ditt innehåll till valfritt CDN och skicka URL:en till Primetime Ad Insertion med Bootstrap API:t.<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## CDN-tokeniseringsscheman som stöds {#cdn-tokenization-schemes}

CDN:er har ofta olika tokeniseringsscheman för fragmentauktorisering. Primetime Ad Insertion stöder aktivt större CDN-nätverk, bland annat:

* Akamai
* Limelight
* Centurylink / Level3
* Kontakta din supportrepresentant på Primetime om du vill ha en fullständig lista över CDN:er som stöds

Mer information om `pttoken` parametern finns i beskrivningen [av](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Bootstrap API-parametern.

## Konfigurera annonser att leverera från innehållets CDN {#configure-ad-deliver-from-cdn}

Ni kanske vill leverera annonser och innehåll från samma CDN för att behålla innehållstillhörigheten, hjälpa till att kringgå annonsblockerare och/eller optimera antalet nödvändiga anslutningar från klientprogrammet. Primetime Ad Insertion har stöd för regler för att skriva om fragment för att mappa fragment till ditt innehålls-CDN.

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## Funktioner för flera CDN {#enable-multi-cdn-fetures}

Kontakta din supportrepresentant på Primetime om du vill aktivera multiCDN-funktioner.
