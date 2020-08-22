---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Hjälp om Primetime Dynamic Ad Insertion
user-guide-description: Explains how to monetize content by inserting user-targeted dynamic ads on the server and engage audience with personalized ads.
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Hjälp för Dynamic Ad Insertion {#ad-insertion}

+ [Översikt över Dynamic Ad Insertion](home.md)
+ [Versionsinformation för Dynamic Ad Insertion](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [Manifest Server Debugging Tool](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ Manifest Server-API för Ad Insertion {#manifest-server}
   + [Översikt över Manifest Server-interaktioner](msapi-topics/ms-overview.md)
   + Kom igång med Manifest Server {#get-started}
      + [Skicka ett kommando till manifestservern](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [Frågeparametrar för Manifest-server](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + Begäranden om annonsinfogning {#ad-insert}
      + [Begäranden om annonsinfogning](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [Valfria frågeparametrar per klient och situation](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [Flera bithastighetsströmmar](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [Inläggning av delvis annonsbrytning](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [Flera CDN-funktioner för CRS och leverans](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + Ersätt VOD-tidslinjer {#replace-vod}
      + [Ändringar i VOD](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [VOD-tidslinjeformat](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [Ersätta en VOD-tidslinje](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + Annonseffektivitetsspårning {#ad}
      + [Annonsspårning](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [Aktivera annonsspårning på klientsidan](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [Översikt över spårning på klientsidan som inte är TVSDK](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [API för spelare som ska interagera med manifestservern](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [EXT-X-MARKER-direktivet](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookies](msapi-topics/ms-cookies.md)
   + [Stöd för WebVTT-bildtexter](msapi-topics/ms-webvtt-captions.md)
   + Lista över filformat {#list}
      + [Filformat](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [JSON-format för URL för begäran om spellista för variantmanifest](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [JSON-format för spårning av URL:er](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [VMAP-format för spårning av URL:er](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [Krav för videospelare](msapi-topics/ms-player-req.md)
+ Primetime Creative Repackaging Service {#crs}
   + [Översikt över CRS](creative-repackaging-service/crs-overview.md)
   + [Huvudsaklig användning av CRS](creative-repackaging-service/jit-async-hls-conv.md)
   + [Stöd för flera CDN](creative-repackaging-service/multi-cdn-supportt.md)
   + [Detaljerade arbetsflöden för JIT-ompaketering](creative-repackaging-service/jit-repackage.md)
   + [Använda CRS för att mata in ID3 Timed Metadata-taggar](creative-repackaging-service/inject-id3.md)
   + [API för ompaketering](creative-repackaging-service/api-repackage.md)
