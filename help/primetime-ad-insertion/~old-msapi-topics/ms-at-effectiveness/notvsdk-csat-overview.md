---
description: Utgivare kan bygga HLS-kompatibla videospelare som fungerar med arbetsflödena för annonsuppföljning på klientsidan i Primetimes manifestfil. Gränssnitten till manifestservern för direktuppspelningen och VOD-fall (video on demand) skiljer sig något åt.
title: Översikt över spårning på klientsidan som inte är TVSDK
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Översikt över spårning på klientsidan som inte är TVSDK {#overview-of-non-tvsdk-client-side-tracking}

Utgivare kan bygga HLS-kompatibla videospelare som fungerar med arbetsflödena för annonsuppföljning på klientsidan i Primetimes manifestfil. Gränssnitten till manifestservern för direktuppspelningen och VOD-fall (video on demand) skiljer sig något åt.

Manifestservern tillhandahåller ett API som gör det möjligt för anpassade spelare att begära följande URL:er, som de kan använda för att rapportera och spåra händelser:

* Annonsintryck
* Annonsartikel
* Annonsstatus
* Content pod progress

Manifestserverns API förutsätter att alla videospelare som använder det uppfyller minimikraven. Se [Krav för videospelare](/help/primetime-ad-insertion/~old-msapi-topics/ms-player-req.md) för mer information.

## Arbetsflöde för spårning på klientsidan {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. Spelaren hämtar en URL till en manifestserver från utgivaren.
1. Player lägger till frågeparametrar som är specifika för annonsinfogningskraven och skickar en HTTP GET-begäran till den resulterande Bootstrap-URL:en. Bootstrap-URL:en har följande syntax:

   ```URL
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   ```

   Till exempel:

   ```URL
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   URL:en innehåller de element som beskrivs i [Skicka ett kommando till manifestservern](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-sending-cmd.md).

1. Manifestservern upprättar en session för spelaren och genererar ett unikt sessions-ID. Den skapar en ny variant av M3U8-spellistans URL, som den returnerar till spelaren som ett JSON-svar. JSON har följande syntax:

   ```JSON
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   ```

   Till exempel:

   ```JSON
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Spelaren använder URL:en från JSON-svaret för att begära den nya varianten av den överordnad spellistan M3U8 från manifestservern.

1. Manifestservern returnerar en ny variant av M3U8 som innehåller URL:er för spellistor på direktuppspelningsnivå med en syntax som liknar följande:

   ```URL
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   ```

   Till exempel:

   ```URL
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Spelaren väljer lämplig URL för single bit rate, manifest på direktuppspelningsnivå för uppspelning av det sammanfogade innehållet. Till exempel:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Manifestservern returnerar ett manifest på strömnivå som innehåller länkar till innehållet och TS-segmentlänkar. Till exempel:

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >Spelaren väljer URL:en till spellistan på direktuppspelningsnivå för att hämta innehållsströmmen. Manifestservern hämtar den ursprungliga spelningslistan från CDN. Vissa kodare kan ge ytterligare information i `#EXTINF` title-attribut, till exempel:
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   Eftersom manifestservern inte kan tolka innebörden av icke-standardattribut för att ändra dem för en sammansatt spellista, tar manifestservern bort alla ytterligare attribut utöver varaktighetsinformationen i den här taggen. Se [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) i HLS-specifikationen för mer information.

1. För att begära spårningsinformation lägger spelaren till frågeparametern `pttrackingposition` med ett alfanumeriskt värde till spellistans URL på direktuppspelningsnivå för den valda bithastigheten. Till exempel:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. Manifestservern returnerar spellistfilen ifylld med antingen en  [JSON](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) eller [VMAP](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) -objektet som innehåller annonsspårningsdata för den m3u8-fil på strömnivå som för närvarande begärs.

   >[!NOTE]
   >
   >Manifestservern genererar bara annonsuppföljningsobjekt om annonser infogades i den aktuella begärda spellistan på strömnivå. Om spelaren spelar upp en spellista som inte innehåller infogade annonser returnerar manifestservern HTTP-status 201 som begäran om spellista för annonsspårning. Om spelaren gör annonsspårningsbegäran för en ström som den inte spelar, returnerar manifestservern HTTP-statusen 500. Om den aktuella uppspelningsbegäran till exempel är för 500.m3u8, returnerar manifestservern en JSON|VMAP i 500.m3u8 som annonsspårningsbegäran. Om spelaren därefter byter strömmar för att spela upp 800.m3u8 blir annonsspårningsinformationen i 500.m3u8 ogiltig, vilket leder till ett 404-fel.

   >[!NOTE]
   >
   >Manifestservern genererar annonsspårningsobjektet baserat på `pttrackingversion` i Bootstrap-URL:en. Om `pttrackingversion` utelämnas eller har ett ogiltigt värde, kommer manifestservern automatiskt att fylla i annonsspårningsinformationen i `#EXT-X-MARKER` -taggar i varje begärd spellista på strömnivå. Se [för mer information](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. Spelaren begär varje annonsspårnings-URL för varje annonsspårningshändelse vid rätt tidpunkt.

>[!NOTE]
>
>För liveströmmar måste spelaren upprepa steg 6 till 10 när paketeraren hela tiden uppdaterar spellistan under liveeventet.

När videon spelas upp måste spelaren spåra spelhuvudets position och använda den här positionen tillsammans med spårnings-URL:er som tagits emot från Primetimes annonsinfogning. Spårnings-URL:erna grupperas efter tidsförskjutning från början av uppspelningen. För varje tidsförskjutning finns det en URL för varje annonssystem som spårningsinformation ska skickas till. Ytterligare information om formatet skiljer sig åt mellan live-video och on demand-video.
