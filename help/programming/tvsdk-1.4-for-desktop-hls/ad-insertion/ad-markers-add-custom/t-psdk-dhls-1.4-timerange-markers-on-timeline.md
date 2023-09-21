---
description: I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.
title: Placera markörer för TimeRange på tidslinjen
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Placera markörer för TimeRange på tidslinjen {#place-timerange-ad-markers-on-the-timeline}

I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.

1. Översätt informationen om annonsplacering utanför band till en lista med `TimeRange` specifikationer (d.v.s. förekomster av `TimeRange` klass).
1. Använd uppsättningen med `TimeRange` specifikationer för att fylla i en instans av `TimeRangeCollection` klassen.
1. Skicka metadatainstansen som kan hämtas från `TimeRangeCollection` -instans, till `replaceCurrentItem` metod (ingår i `MediaPlayer` gränssnitt).
1. Vänta på att TVSDK ska övergå till tillståndet PREPARED genom att vänta på `PlaybackEventListener#onPrepared` återanrop som ska aktiveras.
1. Starta videouppspelning genom att anropa `play()` metod (ingår i `MediaPlayer` gränssnitt).

* Hantera tidslinjekonflikter: Det kan finnas fall där vissa `TimeRange` -specifikationerna överlappar varandra på tidslinjen för uppspelning. Värdet för startpositionen som motsvarar en `TimeRange` Specifikationen kan vara lägre än värdet för den slutposition som redan har monterats. I det här fallet justerar TVSDK i tysthet startpositionen för det felaktiga `TimeRange` för att undvika tidslinjekonflikter. Tack vare den här justeringen har de nya `TimeRange` blir kortare än ursprungligen angivet. Om justeringen är så extrem att den skulle leda till en `TimeRange` med en varaktighet på noll ms, släpper TVSDK i tysthet den felaktiga `TimeRange` -specifikation.

* När `TimeRange` Specifikationer för anpassade annonsuppbrytningar tillhandahålls. TVSDK försöker att översätta dessa till annonser som grupperas inuti annonsbrytningar. TVSDK söker efter angränsande `TimeRange` specifikationer och grupperar dem i separata annonsbrytningar. Om det finns tidsintervall som inte ligger intill något annat tidsintervall, översätts de till annonsbrytningar som innehåller en enda annons.

* Det antas att mediespelarobjektet som läses in pekar på en VOD-resurs. TVSDK kontrollerar detta när programmet försöker läsa in en medieresurs vars metadata innehåller `TimeRange` specifikationer som bara kan användas i samband med den anpassade funktionen för annonsmarkörer. Om den underliggande tillgången inte är av typen VOD genererar TVSDK-biblioteket ett undantag.

* När TVSDK hanterar anpassade annonseringsmarkörer inaktiverar det andra annonslösningsmekanismer (via Adobe Primetime annonsbeslut (tidigare kallat Auditude) eller något annat annonseringssystem). Du kan använda någon av de olika annonslösningsmodulerna i TVSDK eller den anpassade annonseringsmekanismen. När du använder det anpassade API:t för annonsmarkörer anses annonsinnehållet vara löst och placerat på tidslinjen.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

Följande kodfragment innehåller ett enkelt exempel där en uppsättning av tre `TimeRange` -specifikationerna placeras på tidslinjen som anpassade annonsmärken.

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
