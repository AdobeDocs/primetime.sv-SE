---
description: Ni kan infoga annonser i VOD-innehåll.
seo-description: Ni kan infoga annonser i VOD-innehåll.
seo-title: Ersätt tidsintervall med en annons
title: Ersätt tidsintervall med en annons
uuid: c1d93389-cba4-4db0-877d-dbdc5183683c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Ersätt tidsintervall med en annons {#replace-time-ranges-with-an-ad}

Ni kan infoga annonser i VOD-innehåll.

`TimeRanges` mellan `begin` och `end` i `localTime` har tagits bort från tidslinjen. Intervallen ersätts med `AdBreak` av `begin` till `begin+replaceDuration`. Om `replacement-duration` inte finns som parameter gör servern bestämningen på den returnerade `Adbreak`.

>[!TIP]
>
>Du bör alltid ange `replacement-duration` för anpassade intervall. Om inga annonser är avsedda att ersätta det här anpassade intervallet anger du `replacement-duration` 0.

1. Så här ersätter du intervall med Primetime-annonser:

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
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
                       }
                   ]
               },
               "ad": {
                   "targeting": [
                       {
                           "value": "MulAdsAvail12346",
                           "key": "osmfKeyMulAdsAvail12346"
                       }
                   ],
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
