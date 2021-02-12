---
title: Manifest Server Debugging Tool
seo-title: Manifest Server Debugging Tool
description: Manifest Server Debugging Tool
seo-description: Manifest Server Debugging Tool
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 0%

---


# Manifest Server Debugging Tool {#manifest-server-debugging-tool}

Med felsökningsverktyget kan utgivaren undersöka eventuella kostsamma problem med annonsinfogning genom att undersöka felsökningsinformation som returnerats i realtid av manifestservern i HTTP-huvuden eller, när mer detaljerad information behövs, undersöka sessionsloggar efter felet. Adobe partners som Akamai kan använda verktyget för att felsöka integreringar med Primetimes annonsbeslut.

Verktyget har stöd för felsökning och infogningsproblem i alla huvudkonfigurationer för manifestservrar och spårning:

* Spårning på klientsidan med en spelare baserad på TVSDK.
* Spårning på klientsidan med en spelare som inte är baserad på TVSDK.
* Spårning på serversidan.

För att stödja alla dessa fall behöver inte verktyget användas eller använder utgivarkoder för spelare.

När du initierar en manifestserversession kan du ställa in en parameter på begärande URL för att be den logga felsökningsinformation. Om du använder olika värden för den parametern kan du även be manifestservern att returnera angivna felsökningsdata i HTTP-rubriker, men rubrikerna kan bara innehålla en begränsad mängd information. Du kan få inloggningsuppgifter från Adobe för att få tillgång till fullständiga loggfiler, som manifestservern sparar regelbundet (t.ex. varje timme) på en arkivserver. När du har inloggningsuppgifter för den servern kan du när som helst komma åt den direkt.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Alternativ för felsökningsverktyget {#debugging-tool-options}

När du anropar felsökningsverktyget har du flera alternativ för vilken information manifestservern returnerar i HTTP-rubriker. Alternativen påverkar inte vad manifestservern placerar i loggfiler.

### Ange ptdebug {#specifying-ptdebug}

När du initierar felsökningsloggning för en manifestserversession kan du lägga till parametern ptdebug i URL:en för begäran och ange följande alternativ för den information som manifestservern returnerar i HTTP-rubriker:

* ptdebug=true Alla poster utom `TRACE_HTTP_HEADER` och de flesta `call/response data` från `TRACE_AD_CALL`-poster.
* ptdebug=AdCall Only TRACE_AD_*type* (till exempel TRACE_AD_CALL) records.
* ptdebug=Header Only TRACE_HTTP_HEADER records.

Alternativen påverkar inte vad manifestservern placerar i loggfilerna. Du har ingen kontroll över det, men loggfilerna är textfiler, så du kan använda en mängd olika verktyg för att extrahera och formatera information som intresserar dig.

Här är ett exempel på HTTP-huvudet som returneras när `ptdebug=Header`. Vissa långa strängar med hexsiffror ersätts med `. . .` för tydlighet.

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## Format för loggposter {#formats-of-log-records}

Varje loggpost har en typ och en uppsättning fält, varav vissa kan vara valfria. Fälten för alla poster fram till posttypen är desamma. De tillhandahåller en tidsstämpel och information om sessionen. Posttypen identifierar vilken typ av händelse som loggas och efterföljande fält innehåller information om den loggade händelsen.

Strukturen för en loggpost är följande:

`datetime request_id session_id zone_id record_type` *andra fält.*

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| datetime | string | Tidsstämpel |
| request_id | string | Begärande-ID som används av manifestservern (unix timestamp) |
| session_id | string | Sessions-ID som används av manifestservern |
| zone_id | heltal | Zon-ID |
| record_type | string | Typ av händelse som loggas |
| andra fält | *** | Beroende på typ av händelse |

### TRACE_REQUEST_INFO-poster {#trace-request-info-records}

Poster av den här typen loggar resultaten av HTTP-begäranden. Fält efter TRACE_REQUEST_INFO visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| request_method | string | HTTP-metod (GET eller POST) |
| request_uri | string | URI för HTTP-begäran (utan värd) |
| request_length | heltal | Förfrågans längd (byte) |
| response_length | heltal | Svarets längd (byte) |
| delta | heltal | Tid (millisekunder) som begäran ska behandlas |
| module_type | string | Variant, Stream eller VOD |
| remote_address_aud_client_ip | string | (se anmärkning) |
| remote_address_x_fwd_for_hdr_key | string | (se anmärkning) |
| remote_host_port | string | (se anmärkning) |

>[!NOTE]
>
>De sista tre fälten är valfria.

Ett exempel:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER-poster {#trace-http-header-records}

Poster av den här typen loggar HTTP-huvuden som utbyts under HTTP-anrop mellan manifestservern och klienten, annonsservern eller innehållsservern. Fält utanför TRACE_HTTP_HEADER visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| request_type | string | Typ av begäran (MAIN eller UNKNOWN) |
| request_response | string | Svarshuvud (begäran eller svar) |
| header_name | string | HTTP-huvudnamn |
| header_value | string | Base64-kodat HTTP-rubrikvärde |

>[!NOTE]
>
>Fälten request_type och header_value är valfria.

Ett exempel:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACE_AD_CALL-poster {#trace-ad-call-records}

Poster av den här typen loggar resultaten av manifestserverannonsbegäranden. Fält utanför TRACE_AD_CALL visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| request_duration | heltal | Tid (millisekunder) från begäran till svar |
| ad_server_query_url | string | URL för annonsanropet, inklusive frågeparametrar |
| ad_system_id | string | Annonssystem, från annonsserverns svar (Auditude om inte angivet) |
| avail_id | string | ID för tillgången, från annonsreferensen i innehållsmanifestfilen (N/A för VOD) |
| avail_duration | tal | Varaktighet (sekunder) för värdesinstansen, från annonsreferensen i innehållsmanifestfilen (N/A för VOD) |
| ad_server_response | string | Base64-kodat svar från annonsservern |

Ett exempel:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT-, TRACE_AD_RESOLVE- och TRACE_AD_REDIRECT-poster {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Poster av den här typen loggar resultaten av annonsförfrågningarna som anges av posttypen. Fält utanför posttypen visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| avail_id | string | ID för tillgången, från annonsfunktionen i innehållsmanifestfilen (live) eller från manifestservern (VOD) |
| ad_type | string | Typ av annons (DIRECT eller REDIRECT) |
| ad_duration | heltal | Annonsens varaktighet (sekunder), från annonsserverns svar |
| ad_content_url | string | URL för annonsens manifestfil, från annonsserverns svar |
| ad_content_url_actual | string | URL för den infogade annonsens manifestfil. Tom för TRACE_AD_REDIRECT. |
| ad_system_id | string | Annonssystem, från annonsserverns svar (Auditude om inte angivet) |
| ad_id | string | ID för annonsen, från annonsserversvaret |
| creative_id | string | ID för den kreativa, från annonsnoden, från annonsserverns svar |
| ad_call_id | string | Används inte. Reserverad för framtida bruk. |
| delta | heltal | Tid (millisekunder) som den här händelsen tar |
| misc | string | Orsak till varför annonsen hoppades över |

>[!NOTE]
>
>Fälten ad_content_url_actual, ad_call_id och misc är valfria.

För TRACE_AD_RESOLVE och TRACE_AD_INSERT gäller URL:en i fältet ad_content_url_actual den omkodade annonsen om en sådan finns. Annars är fältet tomt för TRACE_AD_RESOLVE eller samma som ad_content_url för TRACE_AD_INSERT.

Ett exempel:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### TRACE_TRACKING_URL-poster {#trace-tracking-url-records}

Poster av den här typen loggar resultaten av manifestserverannonsbegäranden. Fält utanför TRACE_TRACKING_URL visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| punkter | tal | Programtidsstämpel. Tid i videon för att anropa URL:en. |
| ad_system | string | Annonssystem (hörsel eller frihjul) |
| url | string | URL-fäst |
| status | string | HTTP-status returnerades från ping |

Ett exempel:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE-poster {#trace-transcoding-no-media-to-transcode-records}

Poster av den här typen loggar en annonsbyrå som saknas. Det enda fältet efter TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE visas i tabellen.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| ad_id | string | Fullständigt kvalificerat annons-ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]`-PROTOKOLL: AUDITUDE,VAST) |

### TRACE_TRANSCODING_REQUESTED records {#trace-transcoding-requested-records}

Poster av den här typen loggar resultaten av omkodningsbegäranden som manifestservern skickar till CRS. Fält efter TRACE_TRANSCODING_REQUESTED visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| ad_id | string | Fullständigt kvalificerat annons-ID |
| ad_manifest_url | string | URL för annonsens manifestfil, från annonsserverns svar |
| creative_type | string | Typ av media |
| flaggor | string | ID3 anger om omkodningsbegäran innehåller en begäran om att lägga till en ID3-tagg |
| target_duration | string | Måltid (sekunder) för den omkodade kreativa |

### TRACE_TRACKING_REQUEST-poster {#trace-tracking-request-records}

Poster av den här typen indikerar en begäran om att utföra spårning på serversidan. Fält efter TRACE_TRACKING_REQUEST visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| tracking_url_count | heltal | Antal spårnings-URL:er |
| start | float | Starttid för PTS-fragment (sekunder med millisekundprecision) |
| end | float | Sluttid för PTS-fragment (sekunder med millisekundprecision) |

### TRACE_TRACKING_REQUEST_URL records {#trace-tracking-request-url-records}

Poster av den här typen har en spårnings-URL för spårning på serversidan. Fält efter TRACE_TRACKING_REQUEST_URL visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| tidsstämpel | float | Tid (sekunder med precision 0,001) i uppspelningssessionen för att pinga spårnings-URL:en |
| ad_system | string | Annonssystem (t.ex. audiude) |
| url | string | URL till ping |

### TRACE_WEBVTT_REQUEST-poster {#trace-webvtt-request-records}

Poster av den här typen loggar begär att manifestservern skapar WEBVTT-bildtexter. Fält efter TRACE_WEBVTT_REQUEST visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| vtt_uri | string | URL för begäran |
| start | float | Delad starttid (sekunder med millisekundprecision) |
| end | float | Delad sluttid (sekunder med millisekundprecision) |

### TRACE_WEBVTT_RESPONSE-poster {#trace-webvtt-response-records}

Registrerar ``of ``den här ``type ``loggen ``responses ``på ``manifest ``servern ``sends ``till ``clients ``i `` `answer` `` till ``requests `` `for` ``WEBVTT ``beskrivningar. Fält efter TRACE_WEBVTT_RESPONSE visas i den ordning som de visas i tabellen, avgränsade `by`flikar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| svar | string | Base64-kodat svar skickat till klienten |

### TRACE_WEBVTT_SOURCE-poster {#trace-webvtt-source-records}

Poster av den här typen loggar svar på begäranden som manifestservern gör för WEBVTT-bildtexter. Fält efter TRACE_WEBVTT_SOURCE visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | Returnerad HTTP-statuskod |
| källa | string | Base64-kodat ursprungligt VTT-innehåll |


### TRACE_MISC-poster {#trace-misc-records}

Poster av den här typen gör att manifestservern kan logga händelser och information som annars inte planerats när den importerar annonser. Fältet efter TRACE_MISC består av en meddelandesträng. Följande meddelanden kan visas:

* Ad ignore:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*sekunder*, ignore=*ignore*, redirectAd=*redirectAd*, priority=*priority*
* Annonsplaceringen returnerade null.
* Reklamen har sammanfogats.
* Annonsanropet misslyckades: *felmeddelande*.
* Lägger till användaragent för att hämta råmanifestet: *user-agent*.
* Lägger till cookie för att hämta Raw-manifestfil: [cookie]
* Felaktig URL *begärt URL-felmeddelande*. (Det gick inte att parsa variant-URL:en)
* Anropad URL: URL *returnerade: svarskod*. (Live-URL)
* Anropad URL: URL *returkod: svarskod*. ( VOD URL)
* Konflikt vid lösning av annonser: antingen en av - mittrullstart eller mittrullslut ligger inom pre-roll eller pre-roll som finns i mittrullen (VOD).
* Ett ohanterat undantag upptäcktes som genererades av hanteraren för URI: *begärande-URL*.
* Genereringen av variantmanifest har slutförts. (Variant)
* Genereringen av variantmanifest har slutförts.
* Undantag vid hantering av VAST-omdirigering *omdirigerings-URL *fel: *felmeddelande*.
* Det gick inte att hämta annonsens spellista för *annonsens manifest-URL*.
* Det gick inte att generera målmanifestet. (HLSManifestResolver)
* Det gick inte att tolka första annonssamtalssvaret: *felmeddelande*.
* Det gick inte att bearbeta *GET|POST *sökvägsbegäran: *begärande-URL*. (Live/VOD)
* Det gick inte att bearbeta begäran om livemanifest: *begärande-URL*. (Live)
* Det gick inte att returnera ett variantmanifest: *felmeddelande*.
* Det gick inte att verifiera grupp-ID: *grupp-ID*.
* Hämtar raw-manifest: *innehålls-URL*. (Live)
* Efter VAST-omdirigering: *omdirigerings-URL*.
* Tomma tillgängliga. (VOD)
* Hittade *nummer *annonser. (VOD)
* HTTP-begäran har tagits emot. (Mycket första meddelande)
* Annonsen ignoreras eftersom skillnaden mellan annonssvarets varaktighet (*annonsens svarstid *sek) och den faktiska annonstiden (*faktisk varaktighet *sek) är större än gränsen. (HLSManifestResolver)
* Ignorerar tillgänglighet som inte gav något ID-värde. (GroupAdResolver.java)
* Ignorerar tillgänglighet som gav ett ogiltigt tidsvärde: *time *för availId = *Tillgängligt ID*.
* Ignorerar tillgänglighet som angav ett ogiltigt tidsvärde: *duration *for availId = *Tillgängligt ID*.
* Initiera ny session. (Variant)
* Ogiltig HTTP-metod. Det måste vara en GET. (VOD)
* Ogiltig HTTP-metod. Spårningsbegäran måste vara en GET. (Live)
* Ogiltig URL *begärt URL-felmeddelande*. (Variant)
* Ogiltig grupp. (HLSManifestResolver)
* Ogiltig begäran. Bildtexten är inte en giltig spårningsbegäran. (VOD)
* Ogiltig begäran. Bildtextbegäran måste göras när sessionen har upprättats. (VOD)
* Ogiltig begäran. Spårningsbegäran måste göras efter att sessionen har upprättats. (VOD)
* Ogiltig serverinstans för överlagringsgrupp-ID: *grupp-ID*. (Live)
* Gränsen för VAST-omdirigeringar har uppnåtts - *tal*.
* Ring annonser: *annonsanrop-URL*.
* Inget manifest hittades för: *innehålls-URL*. (Live)
* Det gick inte att hitta någon matchande tillgänglig för användar-ID: *Tillgängligt ID*. (HLSManifestResolver)
* Ingen uppspelningssession hittades. (HLSManifestResolver)
* Bearbetar VOD-begäran för manifest *innehålls-URL*.
* Bearbetar variant.
* Bearbetar bildtextbegäran för manifest *innehålls-URL*.
* Bearbetar spårningsbegäran. (VOD)
* Omdirigering av annonssvar är tom. ( VASTStAX)
* Begär: *URL*.
* Returnerat felsvar för GET-begäran eftersom ingen uppspelningssession hittades. (VOD)
* Returnerar felsvar för GET-begäran på grund av ett internt serverfel.
* Returnerat felsvar för GET-begäran som anger en ogiltig resurs: *ID för annonsförfrågan*. (VOD)
* Returnerat felsvar för GET-begäran som anger ett ogiltigt eller tomt grupp-ID: *grupp-ID*. (VOD)
* Returnerat felsvar för GET-begäran som anger ett ogiltigt värde för spårningsposition. (VOD)
* Returnerat felsvar för GET-begäran med ogiltig syntax - *begäran URL*. (Live/VOD)
* Returnerar felsvar för begäran med en HTTP-metod som inte stöds: *GET|POST*. (Live/VOD)
* Returnerar manifest från cache. (VOD)
* Servern är överbelastad. Fortsätt utan en förfrågan om sammanfogning. (Variant)
* Börja generera målmanifest. (HLSManifestResolver)
* Börja generera variantmanifest från: *innehålls-URL*. (Variant)
* Sätt ihop annonser i manifest. (VODHLSResolver)
* Försöker sy ihop annons på `HH:MM:SS`: AdPlacement \[adManifestURL=*och Manifest-URL*, durationSeconds=*seconds*, ignore=*ignore*, redirectAd=*redirect ad*, priority=*priority*.]
* Det går inte att hämta annonser på grund av ogiltig tidslinje - returnerade innehållet utan annonser. (VOD)
* Det går inte att hämta annonser - returnerade innehållet utan annonser. (VOD)
* Det gick inte att hämta annonsfrågan och ingen innehålls-URL angavs. (VOD)
* Giltig URL har tagits emot. (VOD/Variant)
* Variant M3U8 hittades inte. (Variant)

### TRACE_TRACKING_URL-poster {#trace-tracking-url-records-1}

Manifestservern genererar poster av den här typen efter att ha anropat en spårnings-URL under arbetsflödet för spårning på serversidan. Fält utanför TRACE_TRACKING_URL visas i den ordning som de visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| punkter | tal | PTS-tid i ström |
| ad_system | string | Annonssystem (hörsel eller frihjul) |
| url | string | URL-fäst |
| läge | string | HTTP-statuskod |

### TRACE_PLAYBACK_PROGRESS-poster {#trace-playback-progress-records}

Manifestservern genererar poster av den här typen när den tar emot en signal om uppspelningsförloppet under arbetsflödet för spårning på serversidan. Fält efter TRACE_PLAYBACK_PROGRESS visas i den ordning som visas i tabellen, avgränsade med tabbar.

| Fält | Typ | Beskrivning |
|--- |--- |--- |
| status | string | HTTP-statuskod |
| bandbredd | heltal | Strömmens bandbredd |
| punkter | heltal | PTS-tid i ström |
| ms_time | heltal | Tid när spårnings-URL genererades av manifestservern |
| url | string | Omdirigerings-URL |
| header_user_agent | string | HTTP User-Agent header |
| header_dnt | heltal | HTTP do-not-track header |
| effective_remote_address | string | IPv4-giltig fjärradress |
| remote_address | string | IPv4-fjärradress |

>[!NOTE]
>
>De sista fyra fälten är valfria.

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.
