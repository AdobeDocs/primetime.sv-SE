---
description: Ersätt en VOD-tidslinje genom att skicka en ny annonsinfogningsbegäran till manifestservern med en lämpligt angiven frågeparameter för tidslinjen.
title: Ersätta en VOD-tidslinje
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Ersätta en VOD-tidslinje {#replace-a-vod-timeline}

Ersätt en VOD-tidslinje genom att skicka en ny annonsinfogningsbegäran till manifestservern med en lämpligt angiven frågeparameter för tidslinjen.

1. Förbered en annonsbegäran på vanligt sätt.
1. Ange `ptcueformat` frågeparameter till DPIScte35.
1. Ange `enableC3` frågeparametern till true eller false efter behov.
1. Skapa en `pttimeline` parameter som använder tidslinjeformatet VOD:
   1. Ange varje innehållsblock (kapitel) med `duration = 0` och `number_of_lots = 1`.
   1. Ange varje annonsblock som vanligt, men ange `lots = 0` för att ta bort en brytning. Ange `duration = 0` om du vill använda annonsbrytningens varaktighet (från M3U8-filen).

## Exempel: Ersätta en VOD-tidslinje

I det här exemplet antas att VOD-innehållet finns i `Original.m3u8` med en tidslinje för `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

Följande manifestserverbegäran ersätter brytningarna i `Original.m3u8` med en 30-sekunders pre-roll, följt av två brott med varaktighet två minuter vardera.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

Följande manifestserverbegäran tar bort brytningarna i `Original.m3u8` och lägger till en 30-sekunders pre-roll och en 30-sekunders post-roll.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
