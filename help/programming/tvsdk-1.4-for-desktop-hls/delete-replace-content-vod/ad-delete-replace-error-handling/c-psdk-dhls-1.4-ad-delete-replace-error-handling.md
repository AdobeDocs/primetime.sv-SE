---
description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.
seo-description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.
seo-title: Hantering av fel vid borttagning och ersättning av annonser
title: Hantering av fel vid borttagning och ersättning av annonser
uuid: ab153591-0011-44b4-87f9-be0302c2295e
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Hantering av borttagning och ersättningsfel {#ad-deletion-and-replacement-error-handling}

TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.

TVSDK hanterar `timeRanges`-fel genom att utföra standardsammanslagning och sortering. Först sorteras kunddefinierade tidsintervall efter *början*-tiden. Baserat på den här sorteringsordningen sammanfogar den sedan intilliggande intervall och sammanfogar dem om det finns delmängder och skärningar mellan intervallen.

TVSDK hanterar fel i tidsintervallet enligt följande:

* Oordning - TVSDK ändrar ordning på tidsintervallen.
* Delmängd - TVSDK sammanfogar delmängder av tidsintervall.
* Överlappa - TVSDK sammanfogar de överlappande tidsintervallen.
* Ersätt intervallkonflikt - TVSDK väljer ersättningstiden från den tidigaste `timeRange` som visas i den grupp som står i konflikt.

TVSDK hanterar konflikter i signaleringsläge enligt följande:

* Om REPLACE-intervall definieras ändrar TVSDK automatiskt signaleringsläget till CUSTOM_RANGE.
* Om du har definierat DELETE-intervall eller MARK-intervall och signaleringsläget är CUSTOM_RANGE, tar TVSDK bort eller markerar dessa intervall. Det finns ingen annonsinfogning i det här fallet.
* Om ett DELETE-intervall eller ett MARK-intervall definierar en ersättningslängd, ignorerar TVSDK den här varaktigheten.

När servern inte returnerar giltig `AdBreaks`:

* TVSDK genererar och bearbetar en `NOPTimelineOperation` för den tomma `AdBreak`. Ingen annons spelas.

## Exempel på tidsintervallfel {#time-range-error-examples}

TVSDK svarar på felaktiga specifikationer för tidsintervall genom att sammanfoga eller ersätta tidsintervallen efter behov.

I följande exempel definieras fyra överlappande tidsintervall för DELETE. TVSDK sammanfogar de fyra tidsintervallen till ett så att det faktiska borttagningsintervallet är mellan 0 och 50.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

I följande exempel definieras fyra REPLACE-tidsintervall med tidsintervall som står i konflikt. I det här fallet ersätter TVSDK 0-50-talet med 25-tal annonser. Den följer den första ersättningslängden i sorteringsordningen, eftersom det finns konflikter i efterföljande intervall.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
