---
description: Ni kan infoga annonser i VOD-innehåll.
title: Ersätt tidsintervall med en annons
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Ersätt tidsintervall med en annons {#replace-time-ranges-with-an-ad}

Ni kan infoga annonser i VOD-innehåll.

The `TimeRanges` mellan `begin` och `end` in `localTime` tas bort från tidslinjen. Intervallen ersätts med en `AdBreak` av `begin` till `begin+replaceDuration`. Om `replacement-duration` finns inte som parameter, servern gör bestämningen på den returnerade `Adbreak`.

>[!TIP]
>
>Du bör alltid ange en `replacement-duration` för anpassade intervall. Om inga annonser är avsedda att ersätta det här anpassade intervallet kan du skapa en `replacement-duration` av 0.

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
