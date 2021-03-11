---
description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
title: Klassen TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Klassen TimeRangeCollection{#timerangecollection-class}

Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

Det definierade värdet för samlingstypen är `MARK_RANGES`, `DELETE_RANGES` och `REPLACE_RANGES`. Du kan skapa `TimeRangeCollection`s med dessa tre typer.
