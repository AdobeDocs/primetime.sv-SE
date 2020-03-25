---
title: Versionsinformation om PTAI 20.3.3
description: Versionsinformationen för PTAI 20.3.3 beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetimes dynamiska annonsinfogning 2020.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Versionsinformation om dynamisk annonsinfogning för Primetime 20.3.3

Versionsinformationen om dynamisk annonsinfogning 20.3.3 beskriver vad som är nytt eller ändrat, vilka problem som har åtgärdats och kända i Primetimes dynamiska annonsinfogning 2020.

## Nyheter i PTAI 20.3.3

**När:** Torsdag den 26 mars 2020 från 03:00 till 04:00 EASTERN

* SSAI 4XX- och 5XX-svar ger nu korrekt CORS-relaterade rubriker, vilket gör att javascript-/webview-klienter kan läsa felsvar.

* Korrigerade ett problem med X-Forwarded-For-huvuden, där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Ett problem med CMAF/demuxed-ljudströmmar där EXT-X-MEDIA-SEQUENCE-nummer i vissa scenarier ökade felaktigt har åtgärdats

## Vad som ändrats i tidigare versioner

### Version

**När:**

### Version

**När:**

## Lösta problem

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens. Till exempel ZD#xxxxx.

**PTAI 20.3.3**

* Problem med X-Forwarded-For-huvuden där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Problem med CMAF/demuxed-ljudströmmar där EXT-X-MEDIA-SEQUENCE-tal ökar felaktigt i vissa scenarier i vissa scenarier

## Kända fel och begränsningar

**PTAI 20.3.3**

Ingen ny begränsning har lagts till.
