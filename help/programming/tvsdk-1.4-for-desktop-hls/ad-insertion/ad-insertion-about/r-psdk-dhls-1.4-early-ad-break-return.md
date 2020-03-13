---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-title: Implementera tidig radbrytning
title: Implementera tidig radbrytning
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementera tidig radbrytning{#implementing-an-early-ad-break-return}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

>[!NOTE] {othertype=&quot;PrRequirements&quot;}
>
>Du måste prenumerera på splice out/in-annonsmarkörerna ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`och `#EXT-X-CUE`).

Här är några krav att tänka på:

* Tolka markörer som `EXT-X-CUE-IN` (eller motsvarande markeringstagg) som visas i de linjära eller FER-strömmarna.

   Registrera markörerna som markör för snabb annonsretur. Spela endast upp `adBreaks` tills den här markörpositionen visas under uppspelning, vilket åsidosätter längden på den `adBreak` som markeras av den inledande `EXE-X-CUE-OUT` markören.

* Om det finns två `EXT-X-CUE-IN` markörer för samma `EXT-X-CUE-OUT` markör är det den första `EXT-X-CUE-IN` markören som räknas.

* Om `EXE-X-CUE-IN` markören visas på tidslinjen utan någon inledande `EXT-X-CUE-OUT` markör tas `EXE-X-CUE-IN` markören bort.

   Om den inledande `EXT-X-CUE-OUT` markören nyligen har flyttats ut från fönstret i en liveström kommer TVSDK inte att svara på det.

* När en annonsbrytning returneras tidigt spelas spelhuvudet upp tills spelhuvudet återgår till den ursprungliga positionen när annonsbrytningen skulle avslutas och fortsätter att spela upp huvudinnehållet från den positionen. `adBreak`

## SpliceOut och SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` och `SpliceIn` markörerna markerar början och slutet av annonsbrytningen. Längden på `SpliceOut` markörtypen kan vara noll och typen av markörmärken kan vara noll och `EXE-X-CUE` typen av `SpliceIn` `EXE-X-CUE` markörmärken slutet av annonsbrytningen. De visas i en tagg och skiljer sig åt beroende på typ.

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

Om längden på `SpliceOut` typen är noll i exemplet med en markör med olika typer, `SpliceOut` `SpliceIn` måste den fungera tillsammans för varje annonsbrytning. För närvarande är en markör med en längd som inte är noll och som inte behöver paras `SpliceOut` `SpliceIn` markörer mer typisk.

**Två separata markörer**

Det vanligaste scenariot är en `SpliceOut` markör med en varaktighet som inte är noll och som inte behöver `SpliceIn` länkningsmarkörerna. Här markeras slutet av annonsbrytningen med en `SpliceIn` parmarkör under uppspelning av annonsbrytningar, men annonsbrytningen förkortas vid `SpliceIn` markörpositionen och huvudinnehållet börjar spelas upp vid den här positionen.

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

