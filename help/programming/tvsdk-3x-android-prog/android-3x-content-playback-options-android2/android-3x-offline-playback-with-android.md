---
description: Nya API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningsstatus när manifest hämtas.
title: Uppspelning offline med Android
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
