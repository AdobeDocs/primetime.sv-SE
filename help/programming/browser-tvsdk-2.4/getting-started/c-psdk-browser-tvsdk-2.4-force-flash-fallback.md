---
description: Flaggan forceflash i källlistan tvingar Flash-återfall för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.
seo-description: Flaggan forceflash i källlistan tvingar Flash-återfall för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.
seo-title: Tvinga Flash-återfall med hjälp av mediekälllistan
title: Tvinga Flash-återfall med hjälp av mediekälllistan
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Tvinga Flash-återfall med hjälp av mediekälllistan{#forcing-the-flash-fallback-using-the-media-source-list}

Flaggan forceflash i källlistan tvingar Flash-återfall för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.

I listan över mediekällor (till exempel i `sources.js` filen) kan du ange `forceflash` till `true`. Exempel:

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

