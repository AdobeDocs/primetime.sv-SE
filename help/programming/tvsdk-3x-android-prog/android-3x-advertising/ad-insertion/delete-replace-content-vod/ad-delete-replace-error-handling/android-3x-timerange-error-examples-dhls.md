---
description: TVSDK svarar på felaktiga specifikationer för tidsintervall genom att sammanfoga eller ersätta tidsintervallen efter behov.
title: Exempel på tidsintervallfel
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Exempel på tidsintervallfel {#time-range-error-examples}

TVSDK svarar på felaktiga specifikationer för tidsintervall genom att sammanfoga eller ersätta tidsintervallen efter behov.

**DELETE tidsintervall**

I följande exempel definieras fyra överlappande tidsintervall för DELETE. TVSDK sammanfogar de fyra tidsintervallen till ett så att det faktiska borttagningsintervallet är mellan 0 och 50.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**REPLACE-tidsintervall**

I följande exempel definieras fyra REPLACE-tidsintervall med tidsintervall som står i konflikt. I det här fallet ersätter TVSDK 0-50-talet med 25-tal annonser. Den följer den första ersättningslängden i sorteringsordningen, eftersom det finns konflikter i efterföljande intervall.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
