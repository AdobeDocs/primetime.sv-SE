---
description: 'Nya API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningsstatus när manifest hämtas. '
seo-description: 'Nya API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningsstatus när manifest hämtas. '
seo-title: Uppspelning offline med Android
title: Uppspelning offline med Android
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Uppspelning offline med Android {#offline-playback-with-android}

Följande API:er har introducerats som instruerar TVSDK att ignorera nätverksanslutningstillståndet när manifest hämtas. Nätverksanslutningstillståndet används vanligtvis vid strömning med adaptiv bithastighet (ABR) för att avgöra om ett reservförsök ska göras eller om nätverket ska återupptas.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Du kan aktivera den här inställningen och ignorera nätverksanslutningen.

Ange `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` som true. Standardvärdet för ett booleskt värde är false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
