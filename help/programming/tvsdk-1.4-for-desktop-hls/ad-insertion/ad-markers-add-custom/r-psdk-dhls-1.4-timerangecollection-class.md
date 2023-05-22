---
description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
title: Klassen TimeRangeCollection
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

Det definierade värdet för samlingstypen är `MARK_RANGES`, `DELETE_RANGES`och `REPLACE_RANGES`. Du kan skapa `TimeRangeCollection`Dessa tre typer används.
