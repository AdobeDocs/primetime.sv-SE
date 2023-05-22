---
title: JSON-objekt för Primetime-annonser
description: Kodblocket nedan definierar JSON-objektet details när typvärdet är Primetime ads.
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# JSON-objekt för Primetime-annonser {#json-object-for-primetime-ads}

Kodblocket nedan definierar JSON-objektet details när typvärdet är Primetime ads.

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| Egenskap | Beskrivning |
|---|---|
| domän | Primetime-annonsdomänen som ska användas för annonsförfrågningar. |
| medelmåttig | Median som har skapats i Primetime-annonser för det här innehållet. |
| zoneid | The Primetime ads zoneid. Mer information finns i dokumentationen för Primetime-annonser. |
| mål | En array med nyckel-/värdepar som används för att rikta specifika annonser för innehållet. |

Se [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) om du vill ha mer information om attributens värde.
