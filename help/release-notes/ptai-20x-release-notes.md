---
title: Versionsinformation om PTAI 20.12.1
description: Versionsinformationen för PTAI beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetime Ad Insertion under 2020.
translation-type: tm+mt
source-git-commit: 6e4d29f3fb85410943b960b179147b2fc2f1e7c4
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---


# Versionsinformation om Primetime Ad Insertion 20.12.1

Versionsinformationen för Primetime Ad Insertion 20.12.1 beskriver vad som är nytt eller ändrat, vilka problem som har lösts och kända problem i Primetime Ad Insertion under 2020.

## Nyheter i PTAI 20.12.1

**När:** tisdag den 8 december 2020 från 01:00 till 04:00 Eastern Time

**Ändringar**

* Innehåller en snabbkorrigering som åtgärdar intermittenta klientanslutningsproblem (5xx) i Primetime Ad Insertion som uppstod 30 november 2020.

### Förbättringar och korrigeringar i tidigare versioner

#### Version 201.11.1

**När:** Torsdag den 5 november 2020 från kl. 02.00 till kl. 05.00 Eastern Time

**Ändringar**

* Underhållsuppdateringar.

#### Version 201.10.2

**När:** torsdag den 29 oktober 2020 från kl. 12.01 till kl. 06.00 Eastern Time

**Ändringar**

* Underhållsuppdateringar.

#### Version 201.10.1

**När:** tisdag den 13 oktober 2020 från 03:00 till 07:00 Eastern Time

**Ändringar**

* Underhållsuppdateringar.

#### Version 20.9.3

**När:** onsdag den 30 september 2020 kl. 3:30 till 18:30 Eastern Time

**Ändringar**

* Bootstrap API-parameter `ptparallelstream` har lagts till. Detta gör att kunder med spelare som begär CMAF-demuxade ljud- eller videoströmmar parallellt kan säkerställa att annonserna i ljud- och videospår är enhetliga. Ange parametervärdet som true om du vill aktivera den här funktionen eller utelämna om du vill inaktivera den.

#### Version 20.9.2

**När:** tisdag den 15 september 2020 från kl. 3:30 till kl. 18:30 (östtid)

**Förbättringar**

* Tillhandahöll stöd för inkludering av icke-linjära annonstyper med `EXT-X-MARKER`-taggar.
Kontakta en supporttekniker om du vill ha mer information eller vill aktivera den här funktionen.

* Tillhandahåller stöd för att begränsa den totala tiden för annonsupplösning om leverantörerna tar för lång tid att svara. Om du vill aktivera begränsning anger du ett värde i millisekunder för bootstrap-API-parametern `ptadtimeout`.

   >[!NOTE]
   >
   >Den här tidsgränsen gäller endast för annonsförfrågningar, inte för annonsförfrågningar.

#### Version 20.9.1

**När:** tisdag den 1 september 2020 mellan kl. 3:30 och kl. 19:30 Eastern Time

**Ändringar**

* Korrigerade problemet för kunder som använde HLS/CMAF, där EXT-X-MAP ibland saknade CDN-token eller EXT-X-MAP-taggar som ibland felaktigt togs bort från DVR-fönstret.

#### Version 20.8.4

**När:** onsdag den 19 augusti 2020 från 03:30 till 07:30 Eastern Time

**Förbättringar och korrigeringar**

Underhållsuppdateringar.

#### Version 20.8.1

**När:** tisdag den 4 augusti 2020 mellan kl. 3:00 och kl. 18:00 Eastern Time

**Förbättringar och korrigeringar**

Underhållsuppdateringar.

#### Version 20.7.1

**När:** Torsdag den 9 juli 2020 från 03:00 till 05:00 Eastern Time

**Nya funktioner och förbättringar**

* Förbättrad SCTE35 för att använda något av Provider Ad Start/End-meddelandena eller Break Start/End-meddelandena för att identifiera referenspunkten.

* X-ADBE-AI-X1-huvudet har uppdaterats med ytterligare information för felsökning.

* Förbättrad metrisk aggregering.

* Förbättrad SSAI Console-kontrollpanel för sessionsstatistik

#### Version 20.6.2

**När:** torsdagen den 18 juni 2020 från 03:00 till 04:00 Eastern Time

**Förbättringar**

Förbättrad synkronisering av strömmar för videoklipp som kräver millisekundprecision. Kontakta Adobe Support om du vill aktivera millisekundprecision för `#EXT-X-PROGRAM-DATE-TIME tags`.

#### Version 20.6.1

**När:** tisdag den 2 juni 2020 från 03:00 till 05:00 Eastern Time

**Nya funktioner**

Kontakta supporten för Adobe om du vill aktivera följande nya funktioner via konfigurationen på serversidan:

* Manifestmanipulation: HLS-segment och resurs-URL:er kan nu omvandlas mellan HTTP och HTTPS för att öka prestandan genom att minska antalet TLS-handskakningar vid backend-begäranden. Den kan också användas för att sammanfoga annons-/innehållsfragment till samma CDN:er.

* VOD med lång form: Förbättrade API:er för att hålla sessionerna levande med VOD-resurser i lång form.

**Felkorrigeringar**

* Ett problem har korrigerats där WebVTT-fragment alltid begärdes under http-protokollet, oavsett vilket protokoll som ursprungligen begärdes.

* Korrigerade ett problem där EXT-X-DISCONTINUITY-taggar togs bort från spellistans överkant när annonser växlades tillbaka till innehåll. Kontakta supporten för Adobe för att aktivera den här korrigeringen.

#### Version 20.5.1

**När:** tisdag den 5 maj 2020 från 04:00 till 05:00 Eastern Time

* Ett problem har korrigerats som säkerställer att korrekta CORS-huvuden anges när rubrikerna If-Modified-Since skickas.

* Felkorrigeringar på CRS-kontrollpanelen.

* Underhållsuppdateringar.

#### Version 20.3.4

**När:** onsdag den 1 april 2020 från 03:00 till 04:00 Eastern Time

* Korrigerade ett problem som gjorde att undertexter inte synkroniserades efter att annonsen infogats i VOD/WebVTT.

* Säkerhetsuppdateringar.

#### Version 20.3.3

**När:** torsdag den 26 mars 2020 från 03:00 till 04:00 Eastern Time

* SSAI 4XX- och 5XX-svar ger nu korrekt CORS-relaterade rubriker, vilket gör att JavaScript-webbvyklienter kan läsa felsvar.

* Korrigerade ett problem med X-Forwarded-For-huvuden, där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Korrigerade ett problem med CMAF/demuxed-ljudströmmar, där EXT-X-MEDIA-SEQUENCE-nummer i vissa scenarier skulle öka felaktigt.

#### Version 20.3.2

**När:** onsdag den 11 mars 2020 från 05:30 till 07:00 Eastern Time

* Förbättrad SCTE35-signalhantering.

* Underhållsuppdateringar.

#### Version 20.3.1

**När:** torsdag den 5 mars 2020 från 02:30 till 04:30 Eastern Time

* Prestandaförbättringar:

   * Stöd för cacheminne har lagts till för både m3u8-manifest för överordnad/media. De här manifesten svarar nu på Cache-Control: public- och Max-Age-rubriker, som ofta kan förbättra videons startprestanda.

   * Stöd har lagts till för att tvinga https-kreatörer att hämta över http, vilket även kan förbättra videostartens prestanda.

* Säkerhets- och underhållsåtgärder.

#### Version 20.2.1

**När:** torsdag den 13 februari 2020 från 04:30 till 05:30 Eastern Time

* Stöd för sammanslagning av annonsmaterial som innehåller flera strömmar med enbart ljud baserat på språk/kodek/bithastighet.
* Mindre prestandaförbättringar och underhållsuppdateringar.

#### Version 20.1.3

**När:** tisdag den 28 januari 2020 från kl. 2:00 till kl. 03:00 Eastern Time

* **VMAP med FER-stöd för nbc CueFormat**

   Konvertera Cues från FER-ström till parametrar för åsidosättning av tidslinje för FW när `ptcueformat=nbc` används och strömmen är en VOD-ström med in-manifest-cues och inbakade annonser.

* Anpassa fältet för användaragent i HTTP Header innan det vidarebefordras till tredjeparts annonsleverantörer/ CDN.

* Filtrera bort kontrolltecken/icke-utskrivbara tecken (ASCII-kod &lt; 32) från HTTP-headers för användare/agent innan de skickas till Auditude och andra annonsleverantörer, CDN. Auditude Ad-Call misslyckades tidigare för sådana ogiltiga rubriker.

* Rensa gamla V1-objekt från NetStorage-grupper för att hålla objektantalet inom säkra Akamai-gränser.

#### Version 20.1.2 (programfix)

**När:** Måndag den 20 januari 2020 från 02:00 till 03:00 Eastern Time

* Underhållsuppdateringar.

#### Version 20.1.1

**När:** onsdag den 15 januari 2020 från 04:00 till 05:00 Eastern Time

* Tjänsten Creative Repackaging erbjuder nu snabbare annonsinfogning genom att automatiskt blockera listor över felaktigt utformade kreatörer.

* Fas 1-stöd har lagts till för det nya SCTE 35-cue-formatet vid annonsinfogning på serversidan.

* Underhållsuppgraderingar.

## Lösta problem {#Resolved-issues}

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens. Exempel, `ZD#xxxxx`.

**PTAI 20.9.1**

* Korrigerade problemet för kunder som använde HLS/CMAF, där EXT-X-MAP ibland saknade CDN-token eller EXT-X-MAP-taggar som ibland felaktigt togs bort från DVR-fönstret.

**PTAI 20.6.1**

* `WebVTT` fragment begärdes alltid under http-protokollet, oavsett vilket protokoll som ursprungligen begärdes.

* `EXT-X-DISCONTINUITY` -taggar tas bort från spelningslistans övre del när du växlar från annonser tillbaka till innehåll. Kontakta supporten för Adobe för att aktivera den här korrigeringen.

**PTAI 20.5.1**

* Problem med CORS-rubriker när sidhuvuden som ändrats sedan skickas.

* Problem i CRS-kontrollpanelen.

**PTAI 20.3.4**

* Ett problem som gjorde att undertexter inte synkroniserades efter annonsinfogning i VOD/WebVTT.

**PTAI 20.3.3**

* Problem med X-Forwarded-For-huvuden där IPv6-adresser inte var korrekt URL-kodade när de skickades till annonsservrarna.

* Problem med CMAF/demuxed-ljudströmmar där EXT-X-MEDIA-SEQUENCE-tal ökar felaktigt i vissa scenarier i vissa scenarier

## Kända fel och begränsningar

**PTAI 20.10.1**

Ingen ny begränsning har lagts till.
