---
description: Ni kan infoga annonser i VOD-innehåll.
seo-description: Ni kan infoga annonser i VOD-innehåll.
seo-title: Ersätt tidsintervall med en annons
title: Ersätt tidsintervall med en annons
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ersätt tidsintervall med en annons{#replace-time-ranges-with-an-ad}

Ni kan infoga annonser i VOD-innehåll.

I det här fallet tas `TimeRanges` mellan `begin` och `end` i `localTime` bort från tidslinjen. De ersätts med ett `AdBreak` av `begin` till `begin+replaceDuration`. Om ersättningens varaktighet inte finns som en parameter, bestäms den returnerade Adbreak-koden av servern.

>[!NOTE]
>
>Du bör alltid ange en specifik ersättningslängd för anpassade intervall. Om inga annonser är avsedda att ersätta det anpassade intervallet anger du en ersättningstid på 0.

Ersätt intervall med annonser för Primetimes annonsbeslut.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
                },
                {
                    "begin": 69000,
                    "end": 99000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 251000,
                    "end": 281000,
                    "replacement-duration": 30000
                },
                {
                    "begin": 514000,
                    "end": 544000,
                    "replacement-duration": 30000
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
    "title": "VOD - Replace TimeRange with Auditude Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```

