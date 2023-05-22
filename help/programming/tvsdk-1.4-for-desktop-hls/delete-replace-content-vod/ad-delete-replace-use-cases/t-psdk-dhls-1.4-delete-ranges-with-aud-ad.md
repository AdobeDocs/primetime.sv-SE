---
description: Ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.
title: Ta bort intervall med annonsen Primetime-annons
exl-id: e097f92e-b4ce-4e33-9a71-213cf19188fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '42'
ht-degree: 0%

---

# Ta bort intervall med annonsen Primetime-annons{#delete-ranges-with-primetime-ad-decisioning-ad}

Ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.

Ta bort intervall med en frasannons.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],

        "metadata": {
            "time-ranges": {
                "type": "delete",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 20000
                },
                {
                    "begin": 69000,
                    "end": 99000
                },
                {
                    "begin": 251000,
                    "end": 281000
                },
                {
                    "begin": 514000,
                    "end": 544000
                } ]

            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
                "domain": "sandbox2.auditude.com",
                "mediaid": "psdk_000105",
                "zoneid": "121781"
            }     
        }
    },   
    "title": "VOD - DELETE TimeRange with Adobe Primetime ad decisioningxm-replace_text Phrase Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```
