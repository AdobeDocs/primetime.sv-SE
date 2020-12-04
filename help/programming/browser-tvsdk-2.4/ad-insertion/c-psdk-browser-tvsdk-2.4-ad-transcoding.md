---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.
seo-description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.
seo-title: Annonser som inte är kompatibla med ompaketering (trancode)
title: Annonser som inte är kompatibla med ompaketering (trancode)
uuid: f414d133-2d04-462c-ae2c-75158a577fc5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Annonser som inte är kompatibla med ompaketering (trancode){#repackage-transcode-incompatible-ads}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. progressiv nedladdning av MP4.
