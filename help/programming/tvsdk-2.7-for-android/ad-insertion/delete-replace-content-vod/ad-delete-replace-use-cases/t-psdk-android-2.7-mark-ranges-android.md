---
description: Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.
title: Markera intervall
exl-id: ed13168d-5ee8-4f4b-a72e-a38b6d7f9a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Markera intervall {#mark-ranges}

Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.

The `TimeRanges` mellan `begin` och `end` in `localTime` markeras som `AdBreak` på tidslinjen. Andra annonsinställningar ignoreras.

>[!TIP]
>
>Om du bara vill markera vissa intervall i innehållet som annonser, utan dynamisk annonsinfogning, skapar du en `CustomRangeMetadata` -instans och ange typen som `MARK` med definierade anpassade intervall.

1. Tp-markera intervallen:

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
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
                       }
                    ]
   
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
