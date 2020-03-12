---
description: Du kan ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.
seo-description: Du kan ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.
seo-title: Ta bort intervall
title: Ta bort intervall
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Ta bort intervall {#delete-ranges}

Du kan ta bort `TimeRanges` mellan `begin` och `end` in `localTime` från tidslinjen.

>[!TIP]
>
>Om du bara vill ta bort vissa intervall från innehållet skapar du en `CustomRangeMetadata` instans och anger typen som en `DELETE` åtgärd med de definierade anpassade intervallen.

Annonskartan måste användas enligt annonsserverns definition.

1. Så här tar du bort intervall med annonsen Adobe Primetime:

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
                   "type": "delete",
                   "time-range-list": [
                       {
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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```
