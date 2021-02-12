---
title: Utförlig loggning
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---


# Utförlig loggning {#verbose-logging}

## beskrivningar av ptdebug-/loggningshändelser {#ptdebug-logging-events}

När du initierar felsökningsloggning för en manifestserversession kan du lägga till parametern `ptdebug` i begärande-URL:en för att ange följande alternativ för den information som manifestservern returnerar i HTTP-rubriker:

* `ptdebug=true`
Alla poster utom TRACE_HTTP_HEADER och de flesta anrop-/svarsdata från posterna TRACE_AD_CALL.

* `ptdebug=AdCall`
Endast poster av typen TRACE_AD_ (till exempel TRACE_AD_CALL).

* `ptdebug=Header`
Endast TRACE_HTTP_HEADER-poster.

## Format för loggposter {#log-record-formats}

Varje loggpost har en typ och en uppsättning fält, varav vissa kan vara valfria. Fälten för alla poster fram till posttypen är desamma. De tillhandahåller en tidsstämpel och information om sessionen. Posttypen identifierar vilken typ av händelse som loggas och efterföljande fält innehåller information om den loggade händelsen.

Strukturen för en loggpost är följande:

`datetime request_id session_id zone_id record_type other fields`.

| Fält | Typ | Beskrivning |
|---|---|---|
| datetime | string | Tidsstämpel |
| request_id | string | Begärande-ID som används av manifestservern (Unix-tidsstämpel) |
| session_id | string | Sessions-ID som används av manifestservern |
| zone_id | heltal | Zon |
| record_type | string | Typ av händelse som loggas |
| andra fält | varierar | Beroende på typ av händelse |

Poster av den här typen loggar resultaten av HTTP-begäranden. Fält efter `TRACE_REQUEST_INFO` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod |
| request_method | string | HTTP-metod (GET eller POST) |
| request_uri | string | URI för HTTP-begäran (utan värd) |
| request_length | heltal | Förfrågans längd (byte) |
| response_length | heltal | Svarets längd (byte) |
| delta | heltal | Tid (millisekunder) som begäran ska behandlas |
| module_type | string | Variant, Stream eller VOD |
| remote_address_aud_client_ip | string | **‡** |
| remote_address_x_fwd_for_hdr_key | string | **‡** |
| remote_host_port | string | **‡** |

**‡** De tre sista fälten är valfria.

**Ett exempel**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER-poster {#trace-http-header-records}

Poster av den här typen loggar HTTP-huvuden som utbyts under HTTP-anrop mellan manifestservern och klienten, annonsservern eller innehållsservern. Fält utanför TRACE_HTTP_HEADER visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| request_type | string | Typ av begäran (MAIN eller UNKNOWN) |
| request_response | string | Svarshuvud (begäran eller svar) |
| header_name | string | HTTP-huvudnamn |
| header_value | string | Base64-kodat HTTP-rubrikvärde |

>[!NOTE]
>
>Fälten `request_type` och `header_value` är valfria.

**Ett exempel**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE_AD_CALL-poster {#tracing-ad-call-records}

Poster av den här typen loggar resultaten av manifestserverannonsbegäranden. Fält efter `TRACE_AD_CALL` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod |
| request_duration | heltal | Tid (millisekunder) från begäran till svar |
| ad_server_query_url | string | URL för annonsanropet, inklusive frågeparametrar |
| ad_system_id | string | Annonssystem, från annonsserverns svar (Auditude om inte angivet) |
| avail_id | string | ID för tillgången, från annonsreferensen i innehållsmanifestfilen (N/A för VOD) |
| avail_duration | tal | Varaktighet (sekunder) för värdesinstansen, från annonsreferensen i innehållsmanifestfilen (N/A för VOD) |
| ad_server_response | string | Base64-kodat svar från annonsservern |

Ett exempel:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT-, TRACE_AD_RESOLVE- och TRACE_AD_REDIRECT-poster {#trace-ad-insert-resolve-redirect}

Poster av den här typen loggar resultaten av annonsförfrågningarna som anges av posttypen. Fält utanför posttypen visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod. |
| avail_id | string | ID för tillgången, från annonsfunktionen i innehållsmanifestfilen (live) eller från manifestservern (VOD). |
| ad_type | string | Typ av annons (DIRECT eller REDIRECT). |
| ad_duration | heltal | Annonsens varaktighet (sekunder), från annonsserverns svar. |
| ad_content_url | string | URL för annonsens manifestfil, från annonsserverns svar. |
| **†** ad_content_url_actual | string | URL för den infogade annonsens manifestfil. Tom för TRACE_AD_REDIRECT. |
| ad_system_id | string | Annonssystem, från annonsserverns svar (Auditude om inget anges). |
| ad_id | string | ID för annonsen, från annonsserverns svar. |
| creative_id | string | ID för den kreativa, från annonsnoden, från annonsserverns svar. |
| **†** ad_call_id | string | Används inte. Reserverad för framtida bruk. |
| delta | heltal | Tid (millisekunder) som den här händelsen tar. |
| **†** misc | string | Orsak till varför annonsen hoppades över. |

**†** `ad_content_url_actual`,  `ad_call_id`och  `misc` fält är valfria.

>[!NOTE]
>
>För `TRACE_AD_RESOLVE` och `TRACE_AD_INSERT` är URL:en i fältet `ad_content_url_actual` för den omkodade annonsen om en sådan finns tillgänglig. Annars är fältet tomt för `TRACE_AD_RESOLVE` eller samma som `ad_content_url` för `TRACE_AD_INSERT`.

Ett exempel:

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE-poster {#trace-transcoding-no-media-to-transcode}

Poster av den här typen loggar en annonsbyrå som saknas. Det enda fältet efter `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` visas i tabellen.

| Fält | Typ | Beskrivning |
|---|---|---|
| ad_id | string | Fullständigt kvalificerat annons-ID (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOKOLL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOKOLL: AUDITUDE,VAST) |

Poster av den här typen loggar resultaten av omkodningsbegäranden som manifestservern skickar till CRS. Fält efter `TRACE_TRANSCODING_REQUESTED` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| ad_id | string | Fullständigt kvalificerat annons-ID |
| ad_manifest_url | string | URL för annonsens manifestfil, från annonsserverns svar |
| creative_type | string | Typ av media |
| flaggor | string | ID3 anger om omkodningsbegäran innehåller en begäran om att lägga till en ID3-tagg |
| target_duration | string | Måltid (sekunder) för den omkodade kreativa |

Poster av den här typen indikerar en begäran om att utföra spårning på serversidan. Fält efter `TRACE_TRACKING_REQUEST` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| tracking_url_count | heltal | Antal spårnings-URL:er |
| start | float | Starttid för PTS-fragment (sekunder med millisekundprecision) |
| end | float | Sluttid för PTS-fragment (sekunder med millisekundprecision) |

Poster av den här typen har en spårnings-URL för spårning på serversidan. Fält efter `TRACE_TRACKING_REQUEST_URL` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| tidsstämpel | float | Tid (sekunder med precision 0,001) i uppspelningssessionen för att pinga spårnings-URL:en. |
| ad_system | string | Annonssystem (t.ex. audiude) |
| url | string | URL till ping |

Poster av den här typen loggar begär `WEBVTT`-beskrivningar från manifestservern. Fält efter `TRACE_WEBVTT_REQUEST` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod |
| vtt_uri | string | URL för begäran |
| start | float | Delad starttid (sekunder med millisekundprecision) |
| end | float | Delad sluttid (sekunder med millisekundprecision) |

Poster av den här typen loggsvar som manifestservern skickar till klienter i `answer` till begäranden om `WEBVTT` bildtexter. Fält efter `TRACE_WEBVTT_RESPONSE` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod |
| svar | string | Base64-kodat svar skickat till klienten |

Poster av den här typen loggar svar på begäranden som manifestservern gör för `WEBVTT`-beskrivningar. Fält efter `TRACE_WEBVTT_SOURCE` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | Returnerad HTTP-statuskod |
| källa | string | Base64-kodat ursprungligt VTT-innehåll |

Poster av den här typen gör att manifestservern kan logga händelser och information som annars inte planerats när den importerar annonser. Fältet efter `TRACE_MISC` består av en meddelandesträng. Följande meddelanden kan visas:

* Annonsen ignorerades: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* Annonsplaceringen returnerade null.
* Reklamen har sammanfogats.
* Annonsanropet misslyckades: felmeddelande.
* Lägger till användaragent för att hämta råmanifestet: användaragent.
* Lägger till cookie för att hämta Raw-manifestfil: #
* Felaktig URL begärd URL-felmeddelande. (Det gick inte att parsa variant-URL:en)
* Anropad URL: URL returnerades: svarskod. (Live-URL)
* Anropad URL: URL-returkod: svarskod. ( VOD URL)
* Konflikt vid lösning av annonser: antingen en av - mittrullstart eller mittrullslut ligger inom pre-roll eller pre-roll som finns i mittrullen (VOD).
* Ett ohanterat undantag upptäcktes som genererades av hanteraren för URI: begärande-URL.
* Genereringen av variantmanifest har slutförts. (Variant)
* Genereringen av variantmanifest har slutförts.
* Undantag vid hantering av VAST-omdirigering *omdirigerings-URL *fel: felmeddelande.
* Det gick inte att hämta annonsens spellista för annonsens manifest-URL.
* Det gick inte att generera målmanifestet. (HLSManifestResolver)
* Det gick inte att tolka första annonssamtalssvaret: felmeddelande.
* Det gick inte att bearbeta *GET|POST *sökvägsbegäran: begärande-URL. (Live/VOD)
* Det gick inte att bearbeta begäran om livemanifest: begärande-URL. (Live)
* Det gick inte att returnera ett variantmanifest: felmeddelande.
* Det gick inte att verifiera grupp-ID: grupp-ID.
* Hämtar raw-manifest: innehålls-URL. (Live)
* Efter VAST-omdirigering: omdirigerings-URL.
* Tomma tillgängliga. (VOD)
* *antal* annonser hittades. (VOD)
* HTTP-begäran har tagits emot. (Mycket första meddelande)
* Annonsen ignoreras eftersom skillnaden mellan annonssvarets varaktighet (*annonsens svarstid *sek) och den faktiska annonstiden (*faktisk varaktighet *sek) är större än gränsen. (HLSManifestResolver)
* Ignorerar tillgänglighet som inte gav något ID-värde. (GroupAdResolver.java)
* Ignorerar tillgänglighet som gav ett ogiltigt tidsvärde: *time *för availId = avail ID.
* Ignorerar tillgänglighet som angav ett ogiltigt tidsvärde: *duration *for availId = avail ID.
* Initiera ny session. (Variant)
* Ogiltig HTTP-metod. Det måste vara en GET. (VOD)
* Ogiltig HTTP-metod. Spårningsbegäran måste vara en GET. (Live)
* Felmeddelande om en ogiltig URL begärd. (Variant)
* Ogiltig grupp. (HLSManifestResolver)
* Ogiltig begäran. Bildtexten är inte en giltig spårningsbegäran. (VOD)
* Ogiltig begäran. Bildtextbegäran måste göras när sessionen har upprättats. (VOD)
* Ogiltig begäran. Spårningsbegäran måste göras efter att sessionen har upprättats. (VOD)
* Ogiltig serverinstans för överlagringsgrupp-ID: grupp-ID. (Live)
* Gränsen för VAST-omdirigeringar har uppnåtts - antal.
* Ring annonser: och anropa URL.
* Inget manifest hittades för: innehålls-URL. (Live)
* Det gick inte att hitta någon matchande tillgänglig för användar-ID: användar-ID. (HLSManifestResolver)
* Ingen uppspelningssession hittades. (HLSManifestResolver)
* Bearbetar VOD-begäran för manifest content URL.
* Bearbetar variant.
* Bearbetar bildtextbegäran för manifest content URL.
* Bearbetar spårningsbegäran. (VOD)
* Omdirigering av annonssvar är tom. ( VASTStAX)
* Begär: URL.
* Returnerat felsvar för GET-begäran eftersom ingen uppspelningssession hittades. (VOD)
* Returnerar felsvar för GET-begäran på grund av ett internt serverfel.
* Returnerat felsvar för GET-begäran som anger en ogiltig resurs: ID för annonsförfrågan. (VOD)
* Returnerat felsvar för GET-begäran som anger ett ogiltigt eller tomt grupp-ID: grupp-ID. (VOD)
* Returnerat felsvar för GET-begäran som anger ett ogiltigt värde för spårningsposition. (VOD)
* Returnerat felsvar för GET-begäran med ogiltig syntax - request URL. (Live/VOD)
* Returnerar felsvar för begäran med en HTTP-metod som inte stöds: GET|POST. (Live/VOD)
* Returnerar manifest från cache. (VOD)
* Servern är överbelastad. Fortsätt utan en förfrågan om sammanfogning. (Variant)
* Börja generera målmanifest. (HLSManifestResolver)
* Börja generera variantmanifest från: innehålls-URL. (Variant)
* Sätt ihop annonser i manifest. (VODHLSResolver)
* Försöker sy ihop annons på `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= seconds, ignore= ignore, redirectAd= redirect ad, priority= priority.\] \(HLSManifestResolver\)
* Det går inte att hämta annonser på grund av ogiltig tidslinje - returnerade innehållet utan annonser. (VOD)
* Det går inte att hämta annonser - returnerade innehållet utan annonser. (VOD)
* Det gick inte att hämta annonsfrågan och ingen innehålls-URL angavs. (VOD)
* Giltig URL har tagits emot. (VOD/Variant)
* Variant M3U8 hittades inte. (Variant)

### TRACE_PLAYBACK_PROGRESS-poster {#trace-playback-progress-records}

Manifestservern genererar poster av den här typen när den tar emot en signal om uppspelningsförloppet under arbetsflödet för spårning på serversidan. Fält efter `TRACE_PLAYBACK_PROGRESS` visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|---|---|---|
| status | string | HTTP-statuskod |
| bandbredd | heltal | Strömmens bandbredd |
| punkter | heltal | PTS-tid i ström |
| ms_time | heltal | Tid när spårnings-URL genererades av manifestservern |
| url | string | Omdirigerings-URL |
| **u_** header_user_agent | string | HTTP User-Agent header |
| **u_** header_dnt | heltal | HTTP do-not-track header |
| **u_** effective_remote_address | string | IPv4-giltig fjärradress |
| **e** remote_address | string | IPv4-fjärradress |

**De sista** fyra fälten är valfria.

## Flera bithastighetsströmmar {#multiple-bitrate-streams}

Klientförfrågningar om annonsinfogning anger vanligtvis mer än en bithastighet i variantens M3U8-formaterade spelningslista. Manifestservern genererar och returnerar en ny variant av M3U8-fil som innehåller en separat M3U8-länk för varje bithastighet. Det genererar också ett unikt grupp-ID som knyter ihop dessa M3U8s.

Manifestservern använder informationen i klientens Bootstrap URL-begäran för att hämta innehållsvariantens spellista. Den genererar en ny variantspellista som innehåller manifestserverlänkar till innehåll på direktuppspelningsnivå. Klienten använder dessa för att konstruera förfrågningar om annonsinfogning. Manifestserverns innehållslänkar på flödesnivå har följande format:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodManifestservern anger det här värdet baserat på innehållets spellisttyp: Live/linear (
`#EXT-X-PLAYLIST-TYPE:EVENT`) eller VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* ****
publisherAssetIDPublisher har ett unikt ID för det specifika innehåll som anges i Bootstrap URL-begäran.

* ****
renderingManifestservern anger detta baserat på 
`BANDWIDTH` innehållsströmmens värde och använder det för att matcha bithastigheten för annonsen med bithastigheten för innehållet. Annonsbithastigheten får inte överskrida bithastigheten för innehållet om inte annonsåtergivningen med den lägsta bithastigheten gör det.

* **groupIDT**
Manifestservern genererar det här värdet och använder det för att se till att annonserna placeras på ett enhetligt sätt, oavsett för vilken bithastighet kunden begär annonser.

* **base64-encoded url of the bit rate**
streamManifestserverns URL-safe base64 kodar innehållsströmmens absoluta URL. Varje ström har en egen URL.

* **Frågeparametrar**
för Query-parametrar finns i Bootstrap URL-begäran.
