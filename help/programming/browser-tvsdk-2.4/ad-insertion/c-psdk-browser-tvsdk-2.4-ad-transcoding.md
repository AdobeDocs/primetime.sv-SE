---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.
title: Annonser som inte är kompatibla med ompaketering (trancode)
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Annonser som inte är kompatibla med ompaketering (trancode){#repackage-transcode-incompatible-ads}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas med innehållsströmmen för HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) eftersom deras videoformat inte är kompatibelt med HLS/DASH. Adobe Primetime annonsinfogning och webbläsarens TVSDK kan som tillval försöka paketera om inkompatibla videor (transkoda) till kompatibla m3u8/mpd-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. progressiv nedladdning av MP4.
