---
description: TVSDK introducerar säker leverans via HTTPS.
title: Säker leverans över HTTPS
exl-id: 41e2c925-2145-4dfd-909a-aec57dbae9cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

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
