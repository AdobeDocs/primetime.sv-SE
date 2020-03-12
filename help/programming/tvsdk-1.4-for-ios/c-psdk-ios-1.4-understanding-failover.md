---
description: Redundanshantering inträffar när en variantspellista har flera renderingar för samma bithastighet och en av renderingarna slutar att fungera. TVSDK växlar mellan renderingar.
seo-description: Redundanshantering inträffar när en variantspellista har flera renderingar för samma bithastighet och en av renderingarna slutar att fungera. TVSDK växlar mellan renderingar.
seo-title: Redundans
title: Redundans
uuid: 53cf611f-59e6-4728-a287-b98907d7f7bb
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Redundans{#failover}

Redundanshantering inträffar när en variantspellista har flera renderingar för samma bithastighet och en av renderingarna slutar att fungera. TVSDK växlar mellan renderingar.

I följande exempel visas en variantspellista med URL:er för växling vid fel med samma bithastighet:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

När TVSDK läser in variantspellistan skapas en kö som innehåller URL:erna för alla återgivningar av innehållet med samma bithastighet. När en begäran om en URL misslyckas använder TVSDK nästa URL med samma bithastighet från redundanskön. Vid ett specifikt fel går TVSDK igenom alla tillgängliga URL:er en gång tills det hittar en som fungerar korrekt eller tills det har försökt att använda alla tillgängliga URL:er. Om TVSDK har försökt att nå alla tillgängliga URL:er och ingen av URL:erna fungerar, slutar TVSDK att försöka spela upp innehållet.

Redundans inträffar endast på M3U8-nivå, vilket betyder:

* För VOD kan redundans bara uppstå när den börjar spela upp och inte efter att uppspelningen har börjat.
* För direktuppspelning kan växling vid fel inträffa mitt i strömmen.

>[!TIP]
>
>TVSDK, i stället för Apple AV Foundation-spelaren, ger hantering av failover.

