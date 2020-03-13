---
description: Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.
seo-description: Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.
seo-title: Markera intervall
title: Markera intervall
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Markera intervall{#mark-ranges}

Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.

I det här fallet markeras `TimeRanges` mellan `begin` och `end` i `localTime` som en `AdBreak` i tidslinjen. Andra annonsinställningar ignoreras.

>[!NOTE]
>
>Om du bara vill markera vissa intervall i innehållet som annonser (utan dynamisk annonsinfogning) skapar du en `CustomRangeMetadata` instans och anger typen som en MARK-åtgärd med de definierade anpassade intervallen.

1. Markera intervall.

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
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
                       "begin": 0,
                       "end": 15000
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
               }
           }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```

