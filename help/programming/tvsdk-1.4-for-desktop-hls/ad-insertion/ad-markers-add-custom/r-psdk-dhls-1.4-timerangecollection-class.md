---
description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
seo-description: Verktygsklassen TimeRangeCollection abstraherar begreppet om en ordnad samling med TimeRange-specifikationer och tillhandahåller tjänster som kan översättas till en Metadata-instans.
seo-title: Klassen TimeRangeCollection
title: Klassen TimeRangeCollection
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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

Det definierade värdet för samlingstypen är `MARK_RANGES`, `DELETE_RANGES`och `REPLACE_RANGES`. Du kan skapa `TimeRangeCollection`bilder med dessa tre typer.
