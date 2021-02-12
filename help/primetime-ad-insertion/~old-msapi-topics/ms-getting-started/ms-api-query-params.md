---
title: Frågeparametrar för Manifest-server
description: Frågeparametrar talar om för manifestservern vilken typ av klient som skickade begäran och vad klienten vill att manifestservern ska göra. Vissa är obligatoriska och andra har särskilda godkända format eller värden.
seo-title: Frågeparametrar för Manifest-server
seo-description: Frågeparametrar talar om för manifestservern vilken typ av klient som skickade begäran och vad klienten vill att manifestservern ska göra. Vissa är obligatoriska och andra har särskilda godkända format eller värden.
uuid: 03632da3-ae20-427c-bd24-4794ab627cc8
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# Frågeparametrar för manifestserver {#ms-query-params}

Frågeparametrar talar om för manifestservern vilken typ av klient som skickade begäran och vad klienten vill att manifestservern ska göra. Vissa är obligatoriska och andra har särskilda godkända format eller värden.

Den fullständiga URL:en består av bas-URL:en följt av ett frågetecken och sedan `parameterName=value`-argument, avgränsade med et-tecken: `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

## Identifierade parametrar {#section_072845B7FA94468C8068E9092983C9E6}

Manifestservern känner igen följande parametrar. De bearbetas eller skickas, tillsammans med alla okända parametrar, till annonsservern.

| Nyckel | Beskrivning | Obligatoriskt | Giltiga värden |
|---|---|---|---|
| `__sid__` | Unikt ID som manifestservern använder för att generera sessions-ID. | Ja | Alfanumerisk |
| g | Typ av klientenhet | När målregler är beroende av enhetstyp | Se listan på [Klienttyper](https://adobeprimetime.zendesk.com). Kräver åtkomst till Zendesk. |
| k | Nyckelord för anpassad annonsinriktning | Nej | URL-säker sträng i formatet `key1=value1;key2=value2;. . .` |
| u | Tillgångs-ID för Primetime och infogning. | Ja | MD5 Hash-värde |
| z | Primetime och infogningszon-ID för resursen. | Ja | Heltal |
| enableC3 | Klienten är i ett C3-fönster. Om true ersätter du endast lokala resurser. i annat fall ersätter du alla tillgängliga. | Nej | Boolean |
| live | Anger om innehållet är en Live- eller VOD-ström (video on demand). | Akamai Ad Scaler- eller iOS Safari-klient. | Boolean |
| `pabimode` | [Aktivera ](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/partial-ad-break-insetion.md) stöd för partiell infogning av annonsradbrytningar. <br> Aktivera om true eller start.<br> Inaktivera om false. | Nej (standard är inaktiverat) | start, true eller false |
| `ptadwindow` | Varaktighet (sekunder) för fönster med stygn annonser: hur långt tillbaka du ska leta efter annonser när en DVR-användare ansluter till strömmen. | Nej (standard = 1800) | 0 till 1800 |
| `ptassetid` | Unikt ID för innehållet som tilldelas och underhålls av utgivaren. | Akamai Ad Scaler | URL-säker sträng |
| `ptcdn` | Lista över ett eller flera CDN:er som ska vara värd för omkodade resurser. Se [Multi CDN-stöd](/help/primetime-ad-insertion/~old-creative-repackaging-service/multi-cdn-supportt.md). | Nej (default=Akamai) | Exempel: Akamai, Level3, Limelight, Comcast |
| `ptcueformat` | Namnet på det anpassade annonsreferenformatet som finns i M3U8. | Nej | DPISimple, DPIScte35, Elemental, NBC, NFL eller Turner |
| `ptfailover` | Signalerar manifestservern för att identifiera primära strömmar och failover-strömmar som anges i den överordnad spellistan och för att behandla dem som osammanhängande uppsättningar. Detta underlättar redundans och förhindrar timingfel. (Endast för Apple HLS-enheter). Se [Underlätta växling av HLS-spelare](/help/primetime-ad-insertion/~old-msapi-topics/ms-insert-ads/hls-switching-to-failover.md). | Nej | true |
| `ptmulticall` | Om detta anges som sant, görs flera Auditude-annonser för FER. en för varje annonsbrytning. Om värdet är false eller om det inte finns något annonsanrop görs ett anrop till granskning för FER. | Nej | Boolean <br> **Obs**: Följande krav: <ul><li>`ptcueformat` parametern måste anges till nbc</li><li>parametern pttimeline ignoreras.</li></ul> |
| `ptplayer` | Spelare som gör begäran. | iOS/Safari | ios-mobileweb |
| `ptrendition` | Automatiskt genererad genom annonsinfogning och används av Akamai. Lägg inte till eller ta bort. | Akamai Ad Scaler |  |
| `pttagds` | Aktivera [EXT-X- DISCONTINUITY- SEQUENCE](https://tools.ietf.org/html/draft-pantos-http-live-streaming-19#section-4.3.3.3)-taggar | Nej | true - manifestservern innehåller en sekvenstagg före innehållet i varje m3u8-fil som skickas. om parametern inte finns eller inte är true, innehåller manifestservern ingen sekvenstagg. |
| `pttimeline` | En sträng som innehåller den önskade tidslinjen för annonsplacering och innehåll, som åsidosätter och bryter i innehållsströmmen. | Nej | [VOD-tidslinje](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md) |
| `pttoken` | Aktivera TS-segmentets auktoriseringstoken.<br> **Obs**: Endast Akamai CDN-token stöds | För TS-segmentauktoriseringstoken | Boolean |
| `pttrackingmode` | Aktivera annonsspårning; antingen anpassad klientsida (enkel), serversida (sstm) eller hybrid (simplesstm). | Nej | enkel, sstm eller simplesstm.<br> **Obs**: Om den här parametern inte ingår, matas #EX-X-MARKER in i manifestet. Se [EXT-X-MARKER-direktivet](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md). |
| `pttrackingposition` | Instruerar manifestservern att endast returnera annonsspårningsinformation. Ange inte den här parametern i Bootstrap-begäran. | Spårning på klientsidan | Alfanumerisk anteckning:  Manifestservern ignorerar alla skickade värden. Om du skickar en null-sträng eller tom sträng returnerar manifestservern M3U8 i stället för spårningsinformation. |
| `pttrackingversion` | Formatversionen av spårningsinformationen på klientsidan. | Spårning på klientsidan | v1, v2, v3 eller vmap |
| `scteTracking` | Hämta M3U8 innan SCTE-spårningsinformation kan hämtas i JSON V2-sidecar. <br>Den här parametern anger för manifestservern att spelaren som hämtar M3U8 behöver SCTE-tagginformation för att kunna hämtas. | Nej (standard: false) | true eller false. <br> **Obs**: SCTE-35-data returneras i JSON-sidecar med följande kombination av frågeparametervärden: <ul><li>`ptcueformat=turner | elemental | nfl | DPIScte35`</li><li>`pttrackingversion=v2`</li><li>`scteTracking=true`</li></ul> |
| `vetargetmultiplier` | Antalet segment från direktpunkten Förskjutningen före rullning konfigureras med: `(vetargetmultiplier * targetduration + vebufferlength`<br/><br/>**Obs**:  Endast live/linjär | Nej (standard:  3.0) | Float |
| `vebufferLength` | Antalet sekunder från direktpunkten. **Obs**: Endast live/linjär. | Nej (standard: 3.0) | Float |