---
description: Verktygsklassen ReplaceTimeRange är ett tillägg till klassen TimeRange som ska användas med CustomRangeMetadata.
seo-description: Verktygsklassen ReplaceTimeRange är ett tillägg till klassen TimeRange som ska användas med CustomRangeMetadata.
seo-title: Klassen ReplaceTimeRange
title: Klassen ReplaceTimeRange
uuid: d554c17a-2bdc-4c4a-bb8f-2d357511bb32
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Klassen ReplaceTimeRange {#replacetimerange-class}

Verktygsklassen ReplaceTimeRange är ett tillägg till klassen TimeRange som ska användas med CustomRangeMetadata.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
