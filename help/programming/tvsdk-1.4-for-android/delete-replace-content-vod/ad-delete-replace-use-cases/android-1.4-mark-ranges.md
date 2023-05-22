---
description: Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.
title: Markera intervall
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Markera intervall{#mark-ranges}

Du kan ange tidsintervall i VOD-innehåll som annonsbrytningar.

I detta fall `TimeRanges` mellan `begin` och `end` in `localTime` markeras som `AdBreak` på tidslinjen. Andra annonsinställningar ignoreras.

>[!NOTE]
>
>Om du bara vill markera vissa intervall i innehållet som annonser (utan dynamisk annonsinfogning) skapar du en `CustomRangeMetadata` och ange typen som en MARK-åtgärd med de definierade anpassade intervallen.

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
