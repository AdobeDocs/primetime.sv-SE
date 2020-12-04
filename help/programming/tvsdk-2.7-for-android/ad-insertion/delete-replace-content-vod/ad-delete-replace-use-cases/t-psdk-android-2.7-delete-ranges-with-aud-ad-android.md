---
description: Du kan ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.
seo-description: Du kan ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.
seo-title: Ta bort intervall
title: Ta bort intervall
uuid: 637829a7-efa8-4b83-9a04-ef01c043621f
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Ta bort intervall{#delete-ranges}

Du kan ta bort TimeRanges mellan början och slutet i localTime från tidslinjen.

>[!TIP]
>
>Om du bara vill ta bort vissa intervall från innehållet skapar du en `CustomRangeMetadata`-instans och anger typen som en `DELETE`-åtgärd med de definierade anpassade intervallen.

Annonskartan måste användas enligt annonsserverns definition.

1. Så här tar du bort intervall med en annons från Adobe Primetime:

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

