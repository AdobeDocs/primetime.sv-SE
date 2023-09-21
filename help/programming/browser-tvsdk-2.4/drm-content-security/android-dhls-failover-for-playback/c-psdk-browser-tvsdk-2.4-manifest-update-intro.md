---
description: Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i mastermanifesten m3u8 för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Browser TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från huvudmanifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
title: Live master-manifest update
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Live master-manifest update{#live-master-manifest-update}

Webbläsarens TVSDK kan identifiera ändrad uppspelningsinformation i mastermanifesten m3u8 för direktuppspelning och uppdatera uppspelningsinformationen medan strömmen spelas upp. Browser TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från huvudmanifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.

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
