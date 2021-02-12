---
title: Integrera ditt CDN
description: Integrera ditt CDN
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Integrera ditt CDN {#integrating-cdn}

Primetime Ad Insertion fungerar som en proxy mellan klientprogrammet och -manifestationerna, inte själva videosegmenten. Distribuera ditt innehåll till valfritt CDN och skicka URL:en till Primetime Ad Insertion med Bootstrap API:t. Mer integreringsinformation finns i [CDN:er](/help/primetime-ad-insertion/technical-reference/supported-cdns.md) som stöds.

## CDN-tokeniseringsscheman {#cdn-tokenization-schemes} som stöds

CDN:er har ofta olika tokeniseringsscheman för fragmentauktorisering. Primetime Ad Insertion stöder aktivt större CDN-nätverk, bland annat:

* Akamai
* Limelight
* Centurylink / Level3
* Kontakta din supportrepresentant på Primetime om du vill ha en fullständig lista över CDN:er som stöds

Mer information om parametern `pttoken` finns i [Bootstrap API-parameterbeskrivning](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Konfigurera annonser att leverera från innehållets CDN {#configure-ad-deliver-from-cdn}

Ni kanske vill leverera annonser och innehåll från samma CDN för att behålla innehållstillhörigheten, hjälpa till att kringgå annonsblockerare och/eller optimera antalet nödvändiga anslutningar från klientprogrammet. Primetime Ad Insertion har stöd för regler för att skriva om fragment för att mappa fragment till ditt innehålls-CDN. Mer information finns i [Manifestet skrivs om](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Öka startprestanda med ditt CDN {#increase-startup-performance}

Mer information finns i [Optimera start-up](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Multi-CDN-funktioner {#enable-multi-cdn-fetures}

Kontakta din supportrepresentant på Primetime om du vill aktivera multiCDN-funktioner.
