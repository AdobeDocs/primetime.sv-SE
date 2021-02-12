---
title: Cachelagring
description: null
translation-type: tm+mt
source-git-commit: 76dc54fabdae400ad708ba83fcf6f7fd5caa2b22
workflow-type: tm+mt
source-wordcount: '105'
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
