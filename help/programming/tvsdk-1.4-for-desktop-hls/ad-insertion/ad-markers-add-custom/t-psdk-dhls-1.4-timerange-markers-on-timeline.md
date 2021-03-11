---
description: I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.
title: Placera markörer för TimeRange på tidslinjen
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Placera markörer för TimeRange på tidslinjen {#place-timerange-ad-markers-on-the-timeline}

I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.

1. Översätt annonsplaceringsinformationen utanför band till en lista med `TimeRange`-specifikationer (d.v.s. instanser av klassen `TimeRange`).
1. Använd uppsättningen `TimeRange`-specifikationer för att fylla i en instans av klassen `TimeRangeCollection`.
1. Skicka metadatainstansen, som kan hämtas från `TimeRangeCollection`-instansen, till metoden `replaceCurrentItem` (ingår i `MediaPlayer`-gränssnittet).
1. Vänta tills TVSDK övergår till tillståndet PREPARED genom att vänta på att återanropet `PlaybackEventListener#onPrepared` ska aktiveras.
1. Starta videouppspelningen genom att anropa metoden `play()` (del av gränssnittet `MediaPlayer`).

* Hantera tidslinjekonflikter: Det kan finnas fall då vissa `TimeRange`-specifikationer överlappar varandra på tidslinjen för uppspelningen. Värdet för startpositionen som motsvarar en `TimeRange`-specifikation kan till exempel vara lägre än värdet för slutpositionen som redan placerats. I det här fallet justerar TVSDK i tysthet startpositionen för den felaktiga `TimeRange`-specifikationen för att undvika tidslinjekonflikter. Genom den här justeringen blir det nya `TimeRange` kortare än det ursprungligen angivna. Om justeringen är så extrem att den skulle leda till en `TimeRange` med en varaktighet på noll ms, släpper TVSDK tyst den felaktiga `TimeRange`-specifikationen.

* När `TimeRange`-specifikationer för anpassade annonsuppbrytningar anges försöker TVSDK att översätta dessa till annonser som är grupperade i annonsbrytningar. TVSDK söker efter närliggande `TimeRange`-specifikationer och grupperar dem i separata annonsbrytningar. Om det finns tidsintervall som inte ligger intill något annat tidsintervall, översätts de till annonsbrytningar som innehåller en enda annons.

* Det antas att mediespelarobjektet som läses in pekar på en VOD-resurs. TVSDK kontrollerar detta när ditt program försöker läsa in en medieresurs vars metadata innehåller `TimeRange`-specifikationer som bara kan användas i kontexten för den anpassade annonsmärkesfunktionen. Om den underliggande tillgången inte är av typen VOD genererar TVSDK-biblioteket ett undantag.

* När TVSDK hanterar anpassade annonseringsmarkörer inaktiverar det andra annonslösningsmekanismer (via Adobe Primetime annonsbeslut (tidigare Auditude) eller något annat annonsprovisioneringssystem). Du kan använda någon av de olika annonslösningsmodulerna i TVSDK eller den anpassade annonseringsmekanismen. När du använder det anpassade API:t för annonsmarkörer anses annonsinnehållet vara löst och placerat på tidslinjen.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

Följande kodfragment innehåller ett enkelt exempel där en uppsättning med tre `TimeRange`-specifikationer placeras på tidslinjen som anpassade annonsmarkörer.

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
