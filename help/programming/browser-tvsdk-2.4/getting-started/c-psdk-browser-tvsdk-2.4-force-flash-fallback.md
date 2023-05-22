---
description: Flaggan forceflash i källlistan tvingar fram Flash som reserv för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.
title: Tvinga Flash-reserv med hjälp av mediekälllistan
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Tvinga Flash-reserv med hjälp av mediekälllistan{#forcing-the-flash-fallback-using-the-media-source-list}

Flaggan forceflash i källlistan tvingar fram Flash som reserv för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.

I listan över mediekällor (till exempel i `sources.js` fil), kan du ange `forceflash` till `true`. Till exempel:

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```
