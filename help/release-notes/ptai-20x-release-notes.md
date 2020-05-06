---
title: Versionsinformation om PTAI 20.3.3
description: Versionsinformation om PTAI 20.5.1 beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetimes dynamiska annonsinfogning 2020.
translation-type: tm+mt
source-git-commit: 2a5866be64895ba13994720bf943dc676c2595bf
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Versionsinformation om dynamisk annonsinfogning för Primetime 20.5.1

Versionsinformationen om dynamisk annonsinfogning 20.5.1 beskriver vad som är nytt eller ändrat, vilka problem som har åtgärdats och kända i Primetimes dynamiska annonsinfogning 2020.

## Nyheter i PTAI 20.5.1

**När:** Tisdagen den 5 maj 2020 från 04:00 till 05:00 EASTERN

* Ett problem har korrigerats för att säkerställa att rätt CORS-huvuden anges när sidhuvuden som ändrats sedan skickas.

* Felkorrigeringar på CRS-kontrollpanelen.

* Underhållsuppdateringar.

## Vad som ändrats i tidigare versioner

### Version 20.3.4

**När:** Onsdagen den 1 april 2020 från 03:00 till 04:00 EASTERN

* Korrigerade ett problem som gjorde att undertexter inte synkroniserades efter att annonsen infogats i VOD/WebVTT.

* Säkerhetsuppdateringar.

### Version 20.3.3

**När:** Torsdag den 26 mars 2020 från 03:00 till 04:00 EASTERN

* SSAI 4XX- och 5XX-svar ger nu korrekt CORS-relaterade rubriker, vilket gör att javascript-/webview-klienter kan läsa felsvar.

* Korrigerade ett problem med X-Forwarded-For-huvuden, där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Korrigerade ett problem med CMAF/demuxed-ljudströmmar, där EXT-X-MEDIA-SEQUENCE-nummer i vissa scenarier skulle öka felaktigt.

### Version 20.1.3

**När:** Tisdagen den 28 januari 2020 från kl. 2:00 till kl. 03:00 EASTERN

* **VMAP med FER-stöd för CueFormat** Convert-cues från FER-ström till parametrar för åsidosättning av FW-tidslinje, när ptcueformat=nbc används och strömmen är en VOD-ström med in-manifest cues och inbakade annonser.

* Anpassa fältet för användaragent i HTTP Header innan det vidarebefordras till annonsleverantörer/CDN från tredje part.

* Filtrera bort kontrolltecken/icke-utskrivbara tecken (ASCII-kod &lt; 32) från HTTP-rubriker som är&quot;user-agent&quot; innan de skickas till Auditude och andra annonsleverantörer, CDN:er. Auditude Ad-Call misslyckades tidigare för sådana ogiltiga rubriker.

* Rensa gamla V1-objekt från NetStorage-grupper för att hålla objektantalet inom säkra Akamai-gränser.

## Lösta problem

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens. Till exempel ZD#xxxxx.

**PTAI 20.3.3**

* Problem med X-Forwarded-For-huvuden där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Problem med CMAF/demuxed-ljudströmmar där EXT-X-MEDIA-SEQUENCE-tal ökar felaktigt i vissa scenarier i vissa scenarier

## Kända fel och begränsningar

**PTAI 20.3.3**

Ingen ny begränsning har lagts till.
