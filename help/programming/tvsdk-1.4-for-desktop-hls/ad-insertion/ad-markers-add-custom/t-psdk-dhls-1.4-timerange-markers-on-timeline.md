---
description: I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.
seo-description: I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.
seo-title: Placera markörer för TimeRange på tidslinjen
title: Placera markörer för TimeRange på tidslinjen
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Placera markörer för TimeRange på tidslinjen {#place-timerange-ad-markers-on-the-timeline}

I det här exemplet visas det rekommenderade sättet att inkludera TimeRange-specifikationer på tidslinjen för uppspelningen.

1. Översätt informationen om annonsplacering utanför band till en lista med `TimeRange` specifikationer (d.v.s. förekomster av `TimeRange` klassen).
1. Använd uppsättningen med `TimeRange` specifikationer för att fylla i en instans av `TimeRangeCollection` klassen.
1. Skicka Metadata-instansen, som kan hämtas från `TimeRangeCollection` instansen, till `replaceCurrentItem` -metoden (en del av `MediaPlayer` gränssnittet).
1. Vänta på att TVSDK ska övergå till tillståndet PREPARED genom att vänta på att återanropet ska aktiveras `PlaybackEventListener#onPrepared` .
1. Starta videouppspelningen genom att anropa `play()` metoden (del av `MediaPlayer` gränssnittet).

* Hantera tidslinjekonflikter: Det kan finnas fall när vissa `TimeRange` specifikationer överlappar varandra på tidslinjen för uppspelning. Värdet för startpositionen som motsvarar en `TimeRange` specifikation kan till exempel vara lägre än värdet för den slutposition som redan har monterats. I det här fallet justerar TVSDK i tysthet startpositionen för den felaktiga `TimeRange` specifikationen för att undvika tidslinjekonflikter. Med den här justeringen blir det nya `TimeRange` kortare än det ursprungligen angivna. Om justeringen är så extrem att den skulle leda till en `TimeRange` längd på noll ms, släpper TVSDK tyst den felaktiga `TimeRange` specifikationen.

* När `TimeRange` specifikationer för anpassade annonsuppbrytningar tillhandahålls försöker TVSDK att översätta dessa till annonser som grupperas inuti annonsbrytningar. TVSDK söker efter närliggande `TimeRange` specifikationer och grupperar dem i separata annonsbrytningar. Om det finns tidsintervall som inte ligger intill något annat tidsintervall, översätts de till annonsbrytningar som innehåller en enda annons.

* Det antas att mediespelarobjektet som läses in pekar på en VOD-resurs. TVSDK kontrollerar detta varje gång programmet försöker läsa in en medieresurs vars metadata innehåller `TimeRange` specifikationer som bara kan användas i kontexten för den anpassade funktionen annonsmarkörer. Om den underliggande tillgången inte är av typen VOD genererar TVSDK-biblioteket ett undantag.

* När TVSDK hanterar anpassade annonseringsmarkörer inaktiverar det andra annonslösningsmekanismer (via Adobe Primetimes annonsbeslut (tidigare Auditude) eller något annat annonsprovisioneringssystem). Du kan använda någon av de olika annonslösningsmodulerna i TVSDK eller den anpassade annonseringsmekanismen. När du använder det anpassade API:t för annonsmarkörer anses annonsinnehållet vara löst och placerat på tidslinjen.
>
><!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->


Följande kodfragment innehåller ett enkelt exempel där en uppsättning med tre `TimeRange` specifikationer placeras på tidslinjen som anpassade annonsmarkörer.

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
