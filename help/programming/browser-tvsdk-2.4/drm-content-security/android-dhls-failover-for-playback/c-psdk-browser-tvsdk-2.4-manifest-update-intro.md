---
description: Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i överordnad m3u8-manifest för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Webbläsarens TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från det överordnad manifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
title: Live överordnad-manifest update
exl-id: 2f89131c-5204-465b-8757-b47e955f5894
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Live överordnad-manifest update{#live-master-manifest-update}

Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i överordnad m3u8-manifest för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Webbläsarens TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från det överordnad manifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.

Följande funktioner stöds:

* Profilantal (öka eller minska)
* Profilbithastigheter (överlappande eller inte överlappande)
* Profiler med URL:er på samma (eller olika) servrar
* Alla redundansstrukturer

Alla följande villkor måste vara uppfyllda:

* Strömmen är live.
* Både tiden och taggen ändras.
* All återgivningsinformation är densamma (förutom att URL:er kan variera).
* DRM-åtkomstinformationen är densamma.
* Segment paketeras runt samma PTS och bildrutegränser i ett litet felintervall.
