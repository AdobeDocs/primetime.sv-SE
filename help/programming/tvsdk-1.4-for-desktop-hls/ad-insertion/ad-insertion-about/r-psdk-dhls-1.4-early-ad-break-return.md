---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
title: Implementera tidig radbrytning
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Implementera tidig radbrytning{#implementing-an-early-ad-break-return}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

>[!NOTE]
>
>Du måste prenumerera på markörerna för att dela ut/lägga till ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`och `#EXT-X-CUE`).

Här är några krav att tänka på:

* Tolka markörer som `EXT-X-CUE-IN` (eller motsvarande markeringstagg) som visas i de linjära eller FER-strömmarna.

   Registrera markörerna som markör för snabb annonsretur. Endast uppspelning `adBreaks` till den här markörpositionen under uppspelningen, som åsidosätter längden på `adBreak` markerad med radavstånd `EXE-X-CUE-OUT` markör.

* Om två `EXT-X-CUE-IN` det finns markörer för samma `EXT-X-CUE-OUT` markör, den första `EXT-X-CUE-IN` som visas är den som räknas.

* Om `EXE-X-CUE-IN` markören visas på tidslinjen utan radavstånd `EXT-X-CUE-OUT` markör, `EXE-X-CUE-IN` markören ignoreras.

   I en liveström, om det ledande `EXT-X-CUE-OUT` markören har nyligen flyttats ut ur fönstret, TVSDK kommer inte att svara på det.

* När man får en tidig radbrytning är `adBreak` spelas upp tills spelhuvudet återgår till den ursprungliga positionen när annonsbrytningen skulle avslutas och fortsätter spela upp huvudinnehållet från den positionen.

## SpliceOut och SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` och `SpliceIn` markerar början och slutet av annonsbrytningen. Längden på `SpliceOut` typ av `EXE-X-CUE` markören kan vara noll och `SpliceIn` typ av `EXE-X-CUE` markerar slutet av annonsbrytningen. De visas i en tagg och skiljer sig åt beroende på typ.

**En markör med olika typer**

Här är till exempel en markör med olika typer:

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

I ett exempel med olika typer av markörer, om längden på `SpliceOut` typen är noll, `SpliceOut` och `SpliceIn` måste fungera tillsammans för varje annonsbrytning. För närvarande är `SpliceOut` markör med en längd som inte är noll och som inte behöver länkas `SpliceIn` markörer är mer typiska.

**Två separata markörer**

Det mer typiska scenariot är en `SpliceOut` markör med en varaktighet som inte är noll och som inte behöver paras `SpliceIn` markörer. Här, ett par `SpliceIn` markerar slutet på annonsbrytningen vid uppspelning av annonsbrytning, men annonsbrytningen förkortas vid `SpliceIn` och huvudinnehållet börjar spelas upp vid den här positionen.

Här är till exempel två separata markörer:

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```
