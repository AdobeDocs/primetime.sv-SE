---
title: Cachning
description: Cachning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP-cachelagring {#caching}

Primetime Ad Insertion respekterar som standard rubriker för HTTP-cachekontroll när både annonskreatörer och innehåll hämtas.  Detta kan drastiskt minska antalet nätverksbegäranden som Primetime Ad Insertion behöver göra till CDN för alla klienter.  För cachelagring rekommenderar Adobe följande inställningar och inkluderar att du skickar HTTP-huvudet `max-age` från ditt CDN.  Kontakta din CDN-representant för att aktivera dessa rubriker i era videoströmmar och annonsströmmar.

## För live/linjärt innehåll {#caching-live-linear-content}

* Huvudmanifest: 24 timmar, eller Cache-Control: max-age=86400
* Mediematerial: 1 sekund eller Cache-Control: max-age=1

## För VOD-innehåll {#caching-vod-content}

* Huvudmanifest: 24 timmar, eller Cache-Control: max-age=86400
* Mediematerial: 24 timmar, eller Cache-Control: max-age=86400
