---
description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.
seo-description: TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.
seo-title: Hantering av fel vid borttagning och ersättning av annonser
title: Hantering av fel vid borttagning och ersättning av annonser
uuid: e2e06f13-9813-4d86-b6fe-3d09f3bdb100
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Hantering av fel vid borttagning och ersättning av annonser{#ad-deletion-and-replacement-error-handling}

TVSDK hanterar fel i tidsintervallet beroende på det specifika problemet, antingen genom att slå samman eller genom att ändra ordning på de felaktigt definierade tidsintervallen.

TVSDK hanterar `timeRanges` fel genom att utföra standardsammanslagning och sortering. För det första sorteras kunddefinierade tidsintervall efter *starttiden* . Baserat på den här sorteringsordningen sammanfogar den sedan intilliggande intervall och sammanfogar dem om det finns delmängder och skärningar mellan intervallen.

TVSDK hanterar fel i tidsintervallet enligt följande:

* Oordning - TVSDK ändrar ordning på tidsintervallen.
* Delmängd - TVSDK sammanfogar delmängder av tidsintervall.
* Överlappa - TVSDK sammanfogar de överlappande tidsintervallen.
* Ersätt intervallkonflikt - TVSDK väljer ersättningstiden från det tidigaste som visas `timeRange` i den grupp som står i konflikt.

TVSDK hanterar signeringslägeskonflikter med annonseringsmetadata enligt följande:

* Om annonseringssignaleringsläget är i konflikt med tidsintervallets metadata har alltid tidsintervallets metadata prioritet. Om till exempel annonseringssignaleringsläget är inställt som cues för servermappning eller manifest, och det också finns MARK-tidsintervall i annonsmetadata, blir resultatet att intervallen markeras och inga annonser infogas.
* För REPLACE-intervall, om signeringsläget är inställt som servermappnings- eller manifest-cues, ersätts intervallen enligt vad som anges i REPLACE-intervallen, och det finns ingen annonsinfogning via servermappnings- eller manifest-cues. Se [Lägga till signaleringsläge](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

När servern inte returnerar giltig `AdBreaks`:

* TVSDK genererar och bearbetar en `NOPTimelineOperation` for the empty `AdBreak`. Ingen annons spelas.

För tidsintervall med liveströmmar:

* Även om den här funktionen för borttagning/ersättning av C3-annonser endast är avsedd att användas för VOD, behandlas tidsintervall även för liveströmmar om det anges i annonsens metadata.

## Exempel på tidsintervallfel {#time-range-error-examples}

TVSDK svarar på felaktiga specifikationer för tidsintervall genom att sammanfoga eller ersätta tidsintervallen efter behov.

I följande exempel definieras fyra överlappande DELETE-tidsintervall. TVSDK sammanfogar de fyra tidsintervallen till ett så att det faktiska borttagningsintervallet är mellan 0 och 50.

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
