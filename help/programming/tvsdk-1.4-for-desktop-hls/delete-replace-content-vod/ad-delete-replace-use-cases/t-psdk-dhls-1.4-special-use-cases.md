---
title: Specialanvändningsfall
description: Specialanvändningsfall
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Specialanvändningsexempel{#special-use-cases}

TVSDK prioriterar anpassade intervallinställningar framför standardannonsinställningar. Om till exempel markeringsintervall definieras, ignoreras annonsens infogningsinställningar. Om REPLACE-intervall är definierade använder TVSDK automatiskt signeringsläget `CustomRanges`.

1. `ReplaceRange` utan ersättningstid

   Om ersättningens varaktighet saknas bestäms den faktiska ersättningstiden av servern. Antalet annonser i denna `AdBreak` bestäms också av servern.

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. Intervall för MARK och DELETE med ersättningstid

   Den extra ersättningstiden ignoreras.
