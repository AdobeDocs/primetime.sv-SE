---
title: Cachelagring
description: Cachelagring
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP-cachelagring {#caching}

Primetime Ad Insertion respekterar som standard rubriker för HTTP-cachekontroll när både annonskreatörer och innehåll hämtas.  Detta kan drastiskt minska antalet nätverksbegäranden som Primetime Ad Insertion behöver göra till CDN för alla klienter.  För cachelagring rekommenderar Adobe följande inställningar och inkluderar att du skickar HTTP-huvudet `max-age` från ditt CDN.  Kontakta din CDN-representant för att aktivera dessa rubriker i era videoströmmar och annonsströmmar.

## För live/linjärt innehåll {#caching-live-linear-content}

* Överordnad manifest: 24 timmar eller Cache-Control: max-age=86400
* Mediematerial: 1 sekund, eller Cache-Control: max-age=1

## För VOD-innehåll {#caching-vod-content}

* Överordnad manifest: 24 timmar eller Cache-Control: max-age=86400
* Mediematerial: 24 timmar eller Cache-Control: max-age=86400
