---
description: Nya API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningsstatus när manifest hämtas.
title: Uppspelning offline med Android
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Uppspelning offline med Android {#offline-playback-with-android}

Följande API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningstillståndet när manifest hämtas. Nätverksanslutningstillståndet används vanligtvis vid strömning med adaptiv bithastighet (ABR) för att avgöra om ett reservförsök ska göras eller om nätverket ska återupptas.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Du kan aktivera den här inställningen och ignorera nätverksanslutningen.

Ange `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` till true. Standardvärdet för ett booleskt värde är false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
