---
description: Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.
title: Klassen TimeRange
exl-id: 9dc2abe1-189a-4ef4-9918-37835014bf1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Klassen TimeRange{#timerange-class}

Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Varje `TimeRange` specifikationen i uppsättningen representerar ett segment på uppspelningstidslinjen som underhålls internt av TVSDK och som måste markeras som en annonsrelaterad period.

The `TimeRange` -klassen är en enkel datastruktur som visar startpositionen och slutpositionen på tidslinjen. De här två skrivskyddade egenskaperna förkortar begreppet tidsintervall på tidslinjen för uppspelningen.

>[!TIP]
>
>Båda värdena uttrycks i millisekunder.

Här är en sammanfattning av klassen TimeRange:

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```
