---
description: Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i överordnad m3u8-manifest för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Webbläsarens TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från det överordnad manifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
seo-description: Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i överordnad m3u8-manifest för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Webbläsarens TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från det överordnad manifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
seo-title: Live överordnad-manifest update
title: Live överordnad-manifest update
uuid: 4b918a73-dacf-465a-82d6-404c6bdb01f2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '245'
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

