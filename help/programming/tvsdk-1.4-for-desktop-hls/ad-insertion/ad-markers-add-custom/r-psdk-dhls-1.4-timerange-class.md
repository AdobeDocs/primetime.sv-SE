---
description: Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.
seo-description: Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.
seo-title: Klassen TimeRange
title: Klassen TimeRange
uuid: 5d0c979e-cc63-4fdd-becc-b0e3987b0891
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Klassen TimeRange{#timerange-class}

Med anpassade annonsmarkörer kan du skicka en uppsättning TimeRange-specifikationer som representerar tidslinjesegment till TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Varje `TimeRange`-specifikation i uppsättningen representerar ett segment på tidslinjen för uppspelning som underhålls internt av TVSDK och som måste markeras som en annonsrelaterad period.

Klassen `TimeRange` är en enkel datastruktur som visar startpositionen och slutpositionen på tidslinjen. De här två skrivskyddade egenskaperna förkortar begreppet tidsintervall på tidslinjen för uppspelningen.

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

