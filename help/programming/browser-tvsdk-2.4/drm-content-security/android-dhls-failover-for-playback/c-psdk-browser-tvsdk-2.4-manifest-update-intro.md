---
description: Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i överordnad m3u8-manifest för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Webbläsarens TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från det överordnad manifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
title: Live överordnad-manifest update
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
* Både tid och tagg ändras.
* All återgivningsinformation är densamma (förutom att URL:er kan variera).
* DRM-åtkomstinformationen är densamma.
* Segment paketeras runt samma PTS och bildrutegränser i ett litet felintervall.

