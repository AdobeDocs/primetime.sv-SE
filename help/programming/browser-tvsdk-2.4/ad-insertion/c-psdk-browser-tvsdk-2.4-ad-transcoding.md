---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.
title: Annonser som inte är kompatibla med ompaketering (trancode)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Annonser som inte är kompatibla med ompaketering (trancode){#repackage-transcode-incompatible-ads}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. progressiv nedladdning av MP4.
