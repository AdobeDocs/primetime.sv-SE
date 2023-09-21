---
title: Versionsinformation om PTAI 19.11.1
description: Versionsinformationen för PTAI 19.11.1 beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetime Ad Insertion under 2019.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Versionsinformation om Primetime Ad Insertion 19.11.1

Versionsinformationen för Primetime Ad Insertion 19.11.1 beskriver vad som är nytt eller ändrat, vilka problem som har lösts och kända problem i Primetime Ad Insertion under 2019.

## Nyheter i PTAI 19.11.1

**När:** Måndagen den 4 november 2019 kl. 12.01 till 01.00 EASTERN

Underhållsuppdateringar

## Vad som har ändrats i tidigare versioner

### Version 19.10.2

**När:** Torsdagen den 31 oktober 2019 från 01:00 till 03:00 Eastern

Underhållsuppdateringar

### Version 19.10.1

**När:**  Tisdagen den 22 oktober 01:00 till 02:00 EASTERN

Underhållsuppdateringar

### Version 19.9.1

**När:** Tisdagen den 10 september 2019 kl. 12.30-02.00 (östlig tid)

Säkerhetsuppdateringar

### Version 19.8.3

**När:** onsdagen den 28 augusti 2019 kl. 12.30 - 01.30 EASTERN

Korrigerade ett fel där Chromecast-spelarna oväntat avslutade uppspelningen när annonssegment släpptes ut från DVR-fönstret.

### Version 19.8.2

**När:** Onsdag 21 augusti 2019 02:00 till 03:00 Eastern Time

* SSAI Dashboard: Avsnittet Sessionsstatistik. Du kan exportera sessionshändelserna via alternativet Hämta CSV.

* Underhållsuppdateringar

### Version 19.8.1

**När:** Tisdag 6 augusti 2019 02:30 Eastern Time till tisdag 6 augusti 2019 04:30 Eastern Time

* SSAI Dashboard: Nya avsnitt, Sessionsstatistik, har lagts till på SSAI Dashboard
   * Om du har sessions-ID för en SSAI-session där felsökningsläget är aktiverat (ptdebug=true), kan du söka efter följande aktivitet som inträffade under den sessionen:
      * Annonsförfrågningar/svar
      * Infogade annonser
      * Avfyrade fyrar (endast spårning på serversidan)

   * Du kan söka efter aktivitet för ett visst sessions-ID upp till 30 dagar efter att SSAI-sessionen ägde rum
   * Du kan exportera händelserna
* Databas: Säkerhetsuppdateringar

### Version 19.7.1

**När:** Onsdag 10 juli

* SSAI: För ptcueformat-värden som stöder EXT-X-CUE-OUT och brytningssignalering i liveströmmar lade du till ett generiskt makro för att skicka data från attribut i taggen EXT-X-ASSET Exempel: Tagg som medföljer taggen #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=News=News,News Program=NewsAt10 Macros: # kan användas för att skicka News (från attributet GENRE) till en annonsanrops-URL # kan användas för att skicka NewsAt10 (från attributet Program) till ett annonsanrop-URL Exception: För bakåtkompatibilitet har # och # samma funktionalitet. Båda makrona kan användas för att skicka värdet för CAID-attributet, efter konvertering av värdet från hex till long. Det långa värdet är 123456789 för det hex-värdet 75BCD15, i ovanstående exempel. Båda makrona används för att skicka 123456789 till en annonsanrops-URL. Makrot börjar alltid med #. Makrot är skiftlägeskänsligt, men attributet i taggen EXT-X-ASSET är inte skiftlägeskänsligt. Både PROGRAM och Program tillåts i taggen EXT-X-ASSET
* SSAI: Konfigurationsändringar för en viss kund för följande:
   * Glidande fönster (spelningslista live) på fyra minuter
   * Om ett timeout-undantag för socket inträffar när Manifest Server hämtar källinnehåll returnerar Manifest Server HTTP response code (404) i stället för 500
* Säkerhetsuppdateringar

### Version 19.6.1

**När:** Onsdagen den 12 juni 2019 kl. 11.30 PST till torsdagen den 13 juni 2019 kl. 12.30 PST

* CRS: Normaliseringsregel för kreatörer från RevJet
   * Lagt till regel för normalisering av kreativ URL för RevJet, som används av CRS och SSAI
   * TVSDK: Om du arbetar med eller planerar att leverera annonser från RevJet måste normaliseringsregler läggas till i JSON-reglerna för CRS för att kunna använda CRS tillsammans med sina kreatörer. Kontakta din tekniska kontoansvarige om du behöver hjälp
* CRS: Normaliseringsregel för kreatörer från Innovid
   * Lagt till regel för normalisering av kreativ URL för Innovid, som används av SSAI
   * Den normaliseringsregel som används av CRS har lagts till i en tidigare version
   * TVSDK: Den normaliseringsregel som ska läggas till i JSON för CRS-regler tillhandahölls efter en tidigare version, men för att vara säker bör du tala med din tekniska kontohanterare för att granska alla normaliseringsregler som finns.
     >[!NOTE]
     >
     >De flesta innovid-kreativa URL:er kommer att kodas om och sammanfogas utan normaliseringsregeln. Ibland kan det dock hända att inaktiva kreativa URL:er med dynamiska parametrar påträffas. Normaliseringsregeln behövs för att hantera dessa instanser.

### Version 19.5.2

**När:** Onsdag 22:30 Eastern Time to onsdag 22:30 Eastern Time 22:30

* Stöd för CMAF (HLS/fMP4-innehåll) har lagts till
   * SSAI: Hantera CMAF-manifest
   * SSAI: Initiera transkodningsbegäranden och hämta CRS-resurser beroende på innehållsformatet (HLS/ts och HLS/fMP4)
   * CRS: Arbetsflöde har lagts till för att paketera om annonser i CMAF-format (HLS/fMP4)
* SSAI: Korrigerade ett fel som förhindrade att omultiplicerade annonser infogades i omultiplexat innehåll, när både innehållet och annonsen inte hade ström med enbart ljud (EXT-X-STREAM-INF)
* SSAI: Stöd för CDN-tokens för Limelight (LLNW) för innehållssegment har lagts till
   * När `pttoken=limelight` eller `pttoken=llnw` läggs till i bootstrap-URL:en, lägger vi till ett hemligt huvud när vi hämtar källmasterspellistan. Sedan lägger vi till frågeparametrarna från LLNW:s X-Adobe-Sig-huvud i innehållssegmenten
* SSAI: Ett annat token-värde har lagts till (`pttoken=centurylink`) för stöd för CenturyLink CDN auth token, som släpptes 30 juli 2018
   * `pttoken=centurylink` har samma beteende som `pttoken=level3`och båda värdena är giltiga

### Version 19.5.1

**När:** Torsdag 9 maj klockan 2:30 Eastern Time till torsdag 9 maj 04:30 Eastern Time

* SSAI: Säkerhetsuppdateringar
* CRS Dashboard: Strängen &quot;FqAdId Sample&quot; trunkerades till 255 tecken på grund av datalagringsbegränsningar (8 bitar)
   * Strängen&quot;FqAdId Sample&quot; innehåller Ad System och Ad ID från alla XML-svar i annonsens wrapper-kedja för infogning av alla CRS-annonser med SSAI (Creative Stats-avsnittet i CRS Dashboard)
* SSAI och CRS Dashboards: Uppdateringar av programvaruversioner

### Version 19.4.1

**När:** Onsdag 10 april 2:30 Eastern Time to onsdag, 10 april 04:30 Eastern Time

* CRS: CRS Repackaging API har inte längre stöd för HTTP-POST-kommandon. API:t för CRS-ompaketering dirigerar automatiskt om (301) HTTP-POST-kommandon till HTTPS
   * Från och med 20 maj inaktiveras HTTP->HTTPS-omdirigering för HTTP-POST-kommandon
   * Om du använder API:t för CRS-ompackning för att paketera om annonser i förväg, ska du byta POST till HTTPS senast 20 maj
* CRS: Omdesignad arkitektur och arbetsflöde för överföring av CRS-resurser till kundernas CDN-ursprung
   * Jobbprocesserna per CDN-ursprung separeras, så överförda flaskhalsar för ett CDN-ursprung påverkar inte överföringar till andra CDN-ursprung
   * Andra fördelar: CRS-jobbbearbetningstider och överföringshastigheten till kundernas CDN-ursprung har förbättrats
* SSAI: Lagt till ClickThrough- och ClickTracking-URL:er för videoannonser i det underordnade JSON v2-formatet
   * En ny JSON-matrisegenskap, &quot;videoClicks&quot;, följer egenskapen &quot;trackingURLs&quot;
   * &quot;event&quot;-värdenamnen är &quot;clickThrough&quot; och &quot;clickTracking&quot;, och de har inget startTime-värde
* SSAI: För CRS-resurser lägger du till funktioner för att förlänga en CRS-tillgångs sökningspost med 30 dagar när den infogas
   * Föregående beteende: Uppslagsposter för CRS-resurser lagras i minnet i varje pod. Uppslagsposter för CRS-resurser tas automatiskt bort 30 dagar efter att de har lagts till i minnet. Om du vill fylla i en återskapares CRS-resursuppslagspost i en ruta efter att den har tagits bort från minnet måste den kreativa personen påträffas tre gånger i den rutan
   * Nytt beteende: När en pod får åtkomst till en CRS-tillgångssökningspost för att infoga CRS-resursen, kommer CRS-resursuppslagspostens förfallotid att förlängas med 30 dagar i den poden. Därför kommer CRS-resurser som används ofta inte att tas bort från ett podcacheminne förrän 30 dagar efter att de senast användes
   * Det nya beteendet är på hela systemet och kan stängas av om en prestandaförsämring upptäcks
* SSAI: Uppdaterat WebVTT-manifestmanipulation endast för liveströmmar
   * Föregående beteende: I WebVTT-manifestet tar du bort EXT-X-DISCONTINUITY-taggar som infogas före varje infogad annons och efter det sista segmentet i den infogade annonsbrytningen
   * Nytt beteende: En ny parameter, vttdisc, med godkända värden som är true och false, har lagts till i startadressen för SSAI
      * vttdisc=true: EXT-X-DISCONTINUITY-taggar infogas i WebVTT-manifestet före varje infogad annons och efter det sista segmentet i den infogade annonsbrytningen, vilket matchar beteendet för ljud-/videomaterial och enbart ljudklipp
      * vttdisc=false (samma som tidigare beteende): I WebVTT-manifestet tar du bort EXT-X-DISCONTINUITY-taggar som infogas före varje infogad annons och efter det sista segmentet i den infogade och brytningen
      * Om parametern vttdisc utelämnas eller har ett annat värde än true/false, kommer vttdisc att ha värdet true som standard
* SSAI: Säkerhetsuppdateringar och programversionsuppdateringar
   * Java: Uppdaterad Java-version med stöd för ytterligare chiffersviter för annonsanrop som utlöses via TLS 1.2 (HTTPS)

### Version 19.2.1

**När:** Onsdagen den 20 februari 2019 1:30 Eastern Time to onsdag den 20 februari 2019 03:30 Eastern Time

* SSAI: Lagt till ClickThrough- och ClickTracking-URL:er för videoannonser i det underordnade JSON v2-formatet
   * Under egenskapen &quot;trackingURLs&quot; blir deras &quot;event&quot;-värdenamn &quot;clickthrough&quot; och &quot;clickTracking&quot;
   * Startvärdet för startTime är början av annonsen
* SSAI: För CRS-resurser lägger du till funktioner för att förlänga en CRS-tillgångs sökningspost med 30 dagar när den infogas
   * Föregående beteende: Uppslagsposter för CRS-resurser lagras i minnet i varje pod. Uppslagsposter för CRS-resurser tas automatiskt bort 30 dagar efter att de har lagts till i minnet. Om du vill fylla i en återskapares CRS-resursuppslagspost i en ruta efter att den har tagits bort från minnet måste den kreativa personen påträffas tre gånger i den rutan
   * Nytt beteende: När en pod får åtkomst till en CRS-tillgångssökningspost för att infoga CRS-resursen, kommer CRS-resursuppslagspostens förfallotid att förlängas med 30 dagar i den poden. Därför kommer CRS-resurser som används ofta inte att tas bort från ett podcacheminne förrän 30 dagar efter att de senast användes
   * Det nya beteendet är på hela systemet och kan stängas av om en prestandaförsämring upptäcks

* SSAI: Programversionsuppdateringar för NGINX och Kafka
   * NGINX och Kafka används för att bränna URL:er för annonsspårning på serversidan och skicka data till SSAI- och CRS Dashboards
* CRS: Prestandaförbättringar av CRS Dashboard

### Webbgränssnittsrelease

**När:** Onsdag 13 februari 04:00 - 16:30 PST

**Vad:** Komponenten Primetime och Decisioning Web UI

* Åtgärda problemet med kalenderanvändargränssnitt där användaren inte kunde välja ett datum efter den 31 december 2018 från kalenderkomponenten när en kampanj eller en rapport byttes ut.

### Version 19.1.2

**När:** Onsdagen den 30 januari 2019 1:30 Eastern Time to onsdag den 30 januari 03:30 Eastern Time

* SSAI: Uppdaterade den söknyckelstruktur som används av SSAI för att lagra och hämta CRS-resurser, för att hantera scenarier där annonsleverantörer har ett dynamiskt annons-ID eller Creative-ID för samma annons
   * Ny uppslagsnyckelstruktur: Zon, Creative URL och formatparametrar (målvaraktighet, utdataformat, mål-CDN)
   * Struktur för gammal söknyckel: Zon, annonssystem, ID, Creative ID, Creative URL och formatparametrar (målvaraktighet, utdataformat, mål-CDN)
   * Uppslagsnycklarna för befintliga CRS-resurser kommer att uppdateras för att matcha den nya strukturen före produktionsreleasen, men observera att nya tillgångar som omkodats mellan uppslagsnyckeluppdateringen och produktionsreleasen kan missas. I så fall initierar de en ny CRS-begäran nästa gång de påträffas efter releasen

* CRS: Lagt till möjlighet att skicka CRS-förfrågningar från blockeringslista/tillåtelselista från specifika annonssystem, annons-ID, kreativa ID:n, kreativa URL:er och/eller kreativa format

  >Anteckning
  >
  >Adobe lägger till blockeringslista regler när annonsleverantörer med dynamiska värden (t.ex. dynamiska parametrar i URL) för samma annons hittas. Sådana blockeringslista-regler inaktiveras när den dynamiska komponenten har lösts, antingen av providern eller via en normaliseringsregel.

   * Om du vill lägga till en blockeringslista- eller tillåtelselista-regel för din zon kan du kontakta din tekniska kontoansvarige för att få hjälp.

### Version 19.1.1

**När:** Onsdag 9 januari 2019 1:30 Eastern Time to onsdag 9 januari 03:30 Eastern Time

* Ett problem har korrigerats där feltolkning av headers för HTTP keep-alive kan resultera i ett fel vid validering av inkommande kreativa resurser som finns på total-stream.net.
* Ett problem har korrigerats där enkla citattecken (&#39;) och dubbla citattecken (&quot;) i Ad ID, Creative ID och andra fält för en ompackningsbegäran gör att ompackningsbegäran misslyckas.
* Växlad till Java long (datatyp) för att åtgärda ett problem där en gräns på 2 147 483 647 i omkodningsvärden för jobb-ID skulle medföra att alla ompaketeringsbegäranden misslyckas.
* Databasoptimeringar.

## Lösta problem

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens. Till exempel ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - Json-svar för CRS-regler cachelagras för att undvika dubblettbegäranden.

## Kända fel och begränsningar

**PTAI 19.7.1**

Ingen ny begränsning har lagts till.
