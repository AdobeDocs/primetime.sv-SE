---
description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
seo-description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
seo-title: Klassen TimeRangeCollection
title: Klassen TimeRangeCollection
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---


# Klassen TimeRangeCollection{#timerangecollection-class}

Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

Parametern `type`, som är den första positionsparametern i signaturen för konstruktormetoderna, är en instans av uppräkningen `TimeRangeCollection#Type`. Detta är en del av klassen `TimeRangeCollection`. De värden som för närvarande definieras av den här uppräkningen är `MARK_RANGES`, `DELETE_RANGES` och `REPLACE_RANGES`. Du kan skapa `TimeRangeCollection`-objekt med dessa tre typer.
