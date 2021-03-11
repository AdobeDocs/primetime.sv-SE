---
description: Du kan ange eller åsidosätta tidslinjer för annonsbrytningar i VOD-innehåll med hjälp av en formaterad lista med annons- och innehållssegment som kallas pods.
title: VOD-tidslinjeformat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# VOD-tidslinjeformat {#vod-timeline-format}

Du kan ange eller åsidosätta tidslinjer för annonsbrytningar i VOD-innehåll med hjälp av en formaterad lista med annons- och innehållssegment som kallas pods.

## Pod {#section_606E9456E25E41C8B8537A023DDD96CE}

En pod är en annonsbrytning eller ett innehållssegment. En tidslinje består av en sekvens med kran, avgränsade med semikolon. Följande typer av poder finns:

### Annonsbrytning

```
B,duration,maximum_number_of_ads,position
```

Varaktigheten anges i sekunder med en precision på 0,001 (millisekunder). antalet annonser är ett heltal. Positionen är något av följande:
* **n** Ingen - ingen annons
* **p** Pre-roll - before the content
* **m** Mid-roll - i innehållet
* **t** Post-roll - efter innehållet

`B,60,2,p` representerar till exempel en brytning på en minut för upp till 2 annonser före innehållet.

### Innehållssegment - kapitel

```
C,duration,number_of_lots
```

Varaktigheten anges i sekunder med en precision på 0,001 (millisekunder). antalet partier (innehållsavsnitt) är ett heltal. `C,300,1` representerar t.ex. en enda femminutersdel av innehållet.