---
title: Bootstrap API
description: 'Bootstrap API '
translation-type: tm+mt
source-git-commit: bf99c76bbbb67560adc675cf84297b8d3b04e19d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

API:t för Bootstrap är vanligtvis den URL som skickas till klient-/videouppspelnings-API:erna.  Information om alternativ och parametrar som kan konfigureras finns i [Bootstrap API-parametrar](#bootstrap-api-parameters).

## Skicka ett kommando till manifestservern {#send-a-command-to-the-manifest-server}

1. Skicka en `HTTP GET`-begäran för en bootstrap-URL som konstruerats med följande mönster:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **Filtillägg** definierat. `.m3u8` om målmanifestet är HLS,  `.mpd` om målmanifesten finns i DASH.

   * **** PublisherAssetIDRequired. Utgivarens unika ID för det specifika innehållet.

   * **Innehållet** URLRequired. URL för M3U8-innehållsfilen, Base64-kodad för att vara säker i manifestserverns URL. Innehålls-URL:en måste peka på en variant M3U8-fil, även om det bara finns en bithastighetsström.

   * **FrågeparametrarDe** här parametrarna utgör den mest varierade delen av begäran. De talar om för manifestservern vilken typ av klient som begär och vad den vill att manifestservern ska göra.

   Exempel:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP vs. HTTPS-begäranden**

   Manifestservern skapar URL:er med samma HTTP-protokoll som klientens begäran. Om en spelare gör en osäker HTTP-begäran (http) returnerar manifestservern URL:er för manifest och Auditude tracking URL:er med http-protokollet. Om en spelare skapar en säker HTTP-anslutning (https), manifestserver, returneras manifest-URL:er och Auditude tracking-URL:er med https-protokollet.

   >[!NOTE]
   >
   >Manifestservern kan inte ändra protokollet (HTTP eller HTTPS) för tredjepartsspårningsbeacons. Du måste kontakta innehållet och tredjeparts- och annonsleverantörer för att få dem att konfigurera önskade protokoll.  Segmentets URL-protokoll kan ändras, men som standard använder du samma protokoll som definieras i måluttrycken.

## Bootstrap API-parametrar {#bootstrap-api-parameters}

Frågeparametrar talar om för manifestservern vilken typ av klient som skickade begäran och vad klienten vill att manifestservern ska göra. Vissa är obligatoriska och andra har särskilda godkända format eller värden.
Den fullständiga URL:en består av bas-URL:en följt av ett frågetecken och sedan `parameterName=value`-argument avgränsade med et-tecken. Exempel, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

Manifestservern känner igen följande parametrar. Alla frågesträngar\
parametrar skickas till annonsservern.

| parameter | description | format |
|---|---|---|
| _sid_ | Ett unikt ID som manifestservern använder för att generera sessions-ID. | Krävs för både DASH/HLS |
| live | Meddelar Primetime Ad Insertion att det skickade innehållsobjektet är en liveström.  Om den här parametern inte skickas kommer Primetime Ad-infogning att göra en sekundär begäran i det inledande manifestanropet för att avgöra om manifestet är live eller vod.<br>Möjliga värden:<br>true för live-<br>innehållfalse för vod <br>contentomit för automatisk identifiering | Valfritt för HLS.  Krävs för DASH |
| z | Zon-ID:t för resursen som måste tillhandahållas Primetime Ad Insertion. Tillhandahålls av din kontoansvarige på Adobe. | Krävs för både DASH/HLS |
| pabimode | Aktiverar [partiell infogning av annonsbrytning](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) för Live-strömmar.<br>Möjliga värden:<br>true för att <br>aktivera inaktivering (standard inaktiverat) | HLS/DASH |
| ptadtimeout | Möjliggör en begränsning av den totala tiden för annonsupplösning om leverantörerna i senare led tar för lång tid att svara.  Långa svar kan orsaka problem med uppspelningen, vilket gör att Primetime DAI kan framtvinga ett svar inom en viss tidsgräns.<br>Möjliga värden:<br>numerisk sträng i millisekunder.<br>utelämna för att inaktivera (standard inaktiverat) | HLS/DASH |
| ptadwindow | Varaktighet (i sekunder) för fönstret för uppslag och beslut - hur långt tillbaka Primetime Ad Insertion kommer att leta efter reklamtips när en DVR-användare ansluter till strömmen. Värdet noll inaktiverar annonsbeslut i mellanrullen i det inledande manifestet, och beslut återupptas först efter den första uppdateringen. Den här parametern är användbar för att inaktivera annonsinfogning i sessioner som bara kan vara i några sekunder (även kanalvänd).<br>Möjliga värden:<br>numerisk sträng 0-1800 (standard 1800) | Endast HLS |
| ptassetid | Unikt ID för innehållet som tilldelas och underhålls av utgivaren.  Krävs när det används tillsammans med Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Lista över ett eller flera CDN:er som ska vara värd för omkodade resurser. Mer information finns i [Leverans och lagring](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Möjliga värden: <br>akamai, level3, line (limelight network), comcast.<br>Som standard används CDN:er för Primetime Ad Insertion. | HLS/DASH |
| ptcueformat | Det angivna formatet för taggar som ska utföra annonsbeslut (till exempel scte35).<br>Möjliga värden:<br>dpisimple, dpiscte35, <br>elementalFör anpassade cue-format kontaktar du din tekniska kontorepresentant för att få det värde du ska använda | HLS/DASH |
| ptfailover | Signalerar manifestservern för att identifiera primära strömmar och failover-strömmar som anges i den överordnad spellistan och för att behandla dem som osammanhängande uppsättningar. Detta underlättar redundans och förhindrar timingfel. (Endast för Apple HLS-enheter.) Mer information finns i [Underlätta växling av HLS-spelare](hls-switching-to-failover.md) | Endast HLS |
| ptmulticall | Om det här alternativet är aktiverat görs en separat annonsbegäran för varje tillgång som hittas i en VOD-resurs.  Som standard försöker Primetime Ad Insertion samla in all tillgänglig information och skicka den till annonsservern på en begäran. Möjliga värden: true för att aktivera, <br>utelämna för att inaktivera (standard inaktiverat) | HLS/DASH |
| ptparallelstream | Gör det möjligt för kunder med spelare som begär CMAF-demultiplexade ljud- eller videoströmmar parallellt för att säkerställa att annonserna i ljud- och videospår är enhetliga. | Endast HLS |
| ptprotoswitch | Aktiverar namngivna regler för omskrivning av manifest och regler för annonshämtning, som vanligtvis kommer att konfigureras av din tekniska supportrepresentant.<br>Exempel: adfetch_fw, cdn_akm | HLS/DASH |
| ptagds | Aktiverar inmatning av EXT-X-DISCONTINUITY-SEQUENCE-taggar i HLS-rubriker.Möjliga värden:true för att inaktivera (standard inaktiverat) | Endast HLS |
| pttimeline | En sträng som innehåller den önskade tidslinjen för annonsplacering och innehåll, som åsidosätter och bryter i innehållsströmmen. [ Se VOD-tidslinjeformat  ] | HLS/DASH |
| pttoken | Aktiverar tokenskyddsscheman för innehållsfragment-/segmentauktoriseringstoken för CDN:er<br>Möjliga värden:<br>akamai, line (limelight), ctl (centurylink) (standardtokenisering är inaktiverat) | HLS/DASH |
| pttrackingmode | Aktivera annonsuppföljningsscheman.<br>Möjliga värden:<br>enkel för klient-side och <br>spårningsstm för server- och <br>spårningsimplesstm för hybridklient/server och spårning (som standard utförs ingen annonsspårning) | HLS/DASH |
| pttrackingposition | Instruerar manifestservern att endast returnera annonsspårningsinformation. Ange inte den här parametern i Bootstrap-begäran.<br>Obs! Manifestservern ignorerar alla skickade värden. Om du skickar en null-sträng eller tom sträng returnerar manifestservern M3U8. | HLS/DASH<br>Spårning på klientsidan |
| pttrackingversion | Anger vilken formatversion som ska returneras.<br>Möjliga värden: <br>v1, v2, v3 eller vmap | HLS/DASH<br>Spårning på klientsidan |
| scteTracking | Den här parametern anger för manifestservern att spelaren som hämtar M3U8 behöver SCTE-tagginformation för att kunna hämtas.<br>Möjliga värden:<br>true eller false (standard false)<br>Obs! SCTE-35-data returneras i JSON-sidecar med följande kombination av frågeparametervärden:<br>ptcueformat=turner | elementärt | nfl | DPIScte35<br>pttackingversion=v2<br>scteTracking=true<br> | Endast HLS |
| veargetmultiplikator | Antalet segment från direktpunkten Förskjutningen före rullning konfigureras med: ( vetargetMultilier * målduration ) + vebufflength<br>Obs! Den här parametern gäller endast för live/linjärt-HLS-strömmar<br>Möjliga värden:<br>numeriskt flyttal<br>(standard: 3.0 - samma som HLS-specifikationen) | Endast HLS |
| vebufferLength | Antalet sekunder från direktpunkten, som används tillsammans med vektamultiplikatorn.<br>Obs! Den här parametern gäller <br>endast för live/linjärt-HLS-strömmarMöjliga värden:<br>numeriskt flyttal<br> (standard: 3.0) | Endast HLS |
