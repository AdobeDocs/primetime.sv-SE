---
title: Versionsinformation om PTAI 20.5.1
description: Versionsinformation om PTAI 20.5.1 beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetimes dynamiska annonsinfogning 2020.
translation-type: tm+mt
source-git-commit: 7c6acf4b310a7df4ea79a5974f66f7f4b615b21c
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Versionsinformation om dynamisk annonsinfogning för Primetime 20.5.1

Versionsinformationen om dynamisk annonsinfogning 20.5.1 beskriver vad som är nytt eller ändrat, vilka problem som har åtgärdats och kända i Primetimes dynamiska annonsinfogning 2020.

## Nyheter i PTAI 20.5.1

**När:** Tisdagen den 5 maj 2020 från 04:00 till 05:00 Eastern Time

* Ett problem har korrigerats som säkerställer att korrekta CORS-huvuden anges när rubrikerna If-Modified-Since skickas.

* Felkorrigeringar på CRS-kontrollpanelen.

* Underhållsuppdateringar.

## Vad som ändrats i tidigare versioner

### Version 20.3.4

**När:** Onsdagen den 1 april 2020 från 03:00 till 04:00 Eastern Time

* Korrigerade ett problem som gjorde att undertexter inte synkroniserades efter att annonsen infogats i VOD/WebVTT.

* Säkerhetsuppdateringar.

### Version 20.3.3

**När:** Torsdagen den 26 mars 2020 från 03:00 till 04:00 Eastern Time

* SSAI 4XX- och 5XX-svar ger nu korrekt CORS-relaterade rubriker, vilket gör att javascript-/webview-klienter kan läsa felsvar.

* Korrigerade ett problem med X-Forwarded-For-huvuden, där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Korrigerade ett problem med CMAF/demuxed-ljudströmmar, där EXT-X-MEDIA-SEQUENCE-nummer i vissa scenarier skulle öka felaktigt.

### Version 20.3.2

**När:** Onsdagen den 11 mars 2020 från 05:30 till 07:00 Eastern Time

* Förbättrad SCTE35-signalhantering.

* Underhållsuppdateringar.

### Version 20.3.1

**När:** Torsdagen den 5 mars 2020 från 02:30 till 04:30 Eastern Time

* Prestandaförbättringar:

   * Stöd för cacheminne har lagts till för både mastermanifest/media m3u8-manifest. De här manifesten svarar nu på Cache-Control: public- och Max-Age-rubriker, som ofta kan förbättra videons startprestanda.

   * Stöd har lagts till för att tvinga https-kreatörer att hämta över http, vilket även kan förbättra videostartens prestanda.

* Säkerhets- och underhållsåtgärder.

### Version 20.2.1

**När:** Torsdag 13 februari 2020 från 04:30 till 05:30 Eastern Time

* Stöd för sammanslagning av annonsmaterial som innehåller flera strömmar med enbart ljud baserat på språk/kodek/bithastighet.
* Mindre prestandaförbättringar och underhållsuppdateringar.

### Version 20.1.3

**När:** Tisdagen den 28 januari 2020 från kl. 02:00 till kl. 03:00 Eastern Time

* **VMAP med FER-stöd för nbc CueFormat**

   Konvertera Cues från FER-ström till parametrar för åsidosättning av tidslinje för FW, när `ptcueformat=nbc` används och strömmen är en VOD-ström med in-manifest cues och inbakade annonser.

* Anpassa fältet för användaragent i HTTP Header innan det vidarebefordras till tredjeparts annonsleverantörer/ CDN.

* Filtrera bort kontrolltecken/icke-utskrivbara tecken (ASCII-kod &lt; 32) från HTTP-headers för användare/agent innan de skickas till Auditude och andra annonsleverantörer, CDN. Auditude Ad-Call misslyckades tidigare för sådana ogiltiga rubriker.

* Rensa gamla V1-objekt från NetStorage-grupper för att hålla objektantalet inom säkra Akamai-gränser.

### Version 20.1.2 [Programfix]

**När:** Måndagen den 20 januari 2020 från 02:00 till 03:00 Eastern Time

* Underhållsuppdateringar.

### Version 20.1.1

**När:** Onsdagen den 15 januari 2020 från 04:00 till 05:00 Eastern Time

* Tjänsten Creative Repackaging erbjuder nu snabbare annonsinfogning genom att automatiskt svartlista oformaterade kreatörer.

* Fas 1-stöd har lagts till för det nya SCTE 35-cue-formatet vid annonsinfogning på serversidan.

* Underhållsuppgraderingar.

## Lösta problem

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens. Exempel: ZD#xxxxx.

**PTAI 20.5.1**

* Problem med CORS-rubriker när sidhuvuden som ändrats sedan skickas.

* Problem i CRS-kontrollpanelen.

**PTAI 20.3.4**

* Ett problem som gjorde att undertexter inte synkroniserades efter annonsinfogning i VOD/WebVTT.

**PTAI 20.3.3**

* Problem med X-Forwarded-For-huvuden där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Problem med CMAF/demuxed-ljudströmmar där EXT-X-MEDIA-SEQUENCE-tal ökar felaktigt i vissa scenarier i vissa scenarier

## Kända fel och begränsningar

**PTAI 20.3.3**

Ingen ny begränsning har lagts till.
