---
description: Ersätt en VOD-tidslinje genom att skicka en ny annonsinfogningsbegäran till manifestservern med en lämpligt angiven frågeparameter för tidslinjen.
seo-description: Ersätt en VOD-tidslinje genom att skicka en ny annonsinfogningsbegäran till manifestservern med en lämpligt angiven frågeparameter för tidslinjen.
seo-title: Ersätta en VOD-tidslinje
title: Ersätta en VOD-tidslinje
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Ersätta en VOD-tidslinje {#replace-a-vod-timeline}

Ersätt en VOD-tidslinje genom att skicka en ny annonsinfogningsbegäran till manifestservern med en lämpligt angiven frågeparameter för tidslinjen.

1. Förbered en annonsbegäran på vanligt sätt.
1. Ställ in frågeparametern `ptcueformat` på DPIScte35.
1. Ställ in frågeparametern `enableC3` på true eller false om det är lämpligt.
1. Skapa en `pttimeline`-parameter med VOD-tidslinjeformatet:
   1. Ange varje innehållsblock (kapitel) med `duration = 0` och `number_of_lots = 1`.
   1. Ange varje annonsblock som vanligt, men ange `lots = 0` för att ta bort en brytning. Ange `duration = 0` för att använda annonsbrytningens varaktighet (från M3U8-filen).

## Exempel: Ersätta en VOD-tidslinje

I det här exemplet antas att VOD-innehållet är i `Original.m3u8` med en tidslinje på `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

Följande manifestserverbegäran ersätter brytningarna i `Original.m3u8` med en 30-sekunders förregistrering, följt av två brytningar med varaktighet två minuter vardera.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

Följande manifestserverbegäran tar bort brytningarna i `Original.m3u8` och lägger till en 30-sekunders förregistrering och en 30-sekunders efterrullning.

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
