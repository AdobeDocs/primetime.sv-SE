---
description: TVSDK introducerar säker leverans via HTTPS.
seo-description: TVSDK introducerar säker leverans via HTTPS.
seo-title: Säker leverans över HTTPS
title: Säker leverans över HTTPS
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# Säker leverans över HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK har stöd för HTTPS-leverans för alla samtal som kommer från TVSDK, som innehåller

* Auditude Ad Server-anrop
* CRS-förfrågningar
* DRM-licensanrop
* Videoanalysens Pings
* Fakturerings-ping

Om du vill använda den här funktionen måste servrarna som konfigurerats för att betjäna ovanstående ha stöd för HTTPS.

Det här nya beteendet är inte aktiverat som standard. Använd följande för att aktivera säker leverans före samtal till `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
