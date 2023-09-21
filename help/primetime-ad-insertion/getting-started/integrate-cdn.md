---
title: Integrera ditt CDN
description: Integrera ditt CDN
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Integrera ditt CDN {#integrating-cdn}

Primetime Ad Insertion fungerar som en proxy mellan klientprogrammet och -manifestationerna, inte själva videosegmenten. Distribuera ditt innehåll till valfritt CDN och skicka URL:en till Primetime Ad Insertion med Bootstrap API:t. Mer information om integrering finns i [CDN:er som stöds](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## CDN-tokeniseringssystem som stöds {#cdn-tokenization-schemes}

CDN:er har ofta olika tokeniseringsscheman för fragmentauktorisering. Primetime Ad Insertion stöder aktivt större CDN-nätverk, bland annat:

* Akamai
* Limelight
* Centurylink / Level3
* Kontakta din supportrepresentant på Primetime om du vill ha en fullständig lista över CDN:er som stöds

Mer information om `pttoken` parameter, se [Beskrivning av Bootstrap API-parameter](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Konfigurera annonser att leverera från innehållets CDN {#configure-ad-deliver-from-cdn}

Ni kanske vill leverera annonser och innehåll från samma CDN för att behålla innehållstillhörigheten, hjälpa till att kringgå annonsblockerare och/eller optimera antalet nödvändiga anslutningar från klientprogrammet. Primetime Ad Insertion har stöd för regler för att skriva om fragment för att mappa fragment till ditt innehålls-CDN. Mer information finns i [Manifestet skrivs om](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Öka startprestanda med ditt CDN {#increase-startup-performance}

Mer information finns i [Optimera starten](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Funktioner för flera CDN {#enable-multi-cdn-fetures}

Kontakta din supportrepresentant på Primetime om du vill aktivera multiCDN-funktioner.
