---
description: Flaggan forceflash i källlistan tvingar fram Flash som reserv för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.
title: Tvinga Flash-reserv med hjälp av mediekälllistan
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Tvinga Flash-reserv med hjälp av mediekälllistan{#forcing-the-flash-fallback-using-the-media-source-list}

Flaggan forceflash i källlistan tvingar fram Flash som reserv för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.

I listan över mediekällor (till exempel i filen `sources.js`) kan du ställa in `forceflash` på `true`. Exempel:

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

