---
description: Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.
title: Klassen TimeRange
exl-id: 7451c4f6-40df-48b2-a2c7-6d7826724716
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Klassen TimeRange{#timerange-class}

Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Varje TimeRange-specifikation i uppsättningen representerar ett segment på tidslinjen som underhålls internt av TVSDK och som måste markeras som en annonsrelaterad period.

The `TimeRange` -klassen är en enkel datastruktur som visar startpositionen och slutpositionen på tidslinjen. De här två skrivskyddade egenskaperna förkortar begreppet tidsintervall på tidslinjen för uppspelningen.

>[!TIP]
>
>Båda värdena uttrycks i millisekunder.

Här är en sammanfattning av `TimeRange` klass:

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```
