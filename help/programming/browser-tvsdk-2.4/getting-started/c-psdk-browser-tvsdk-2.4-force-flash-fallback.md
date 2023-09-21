---
description: Flaggan forceflash i källlistan tvingar fram Flash som reserv för en URL. För den här URL:en kan du använda Adobe Flash Player för att spela upp innehållet.
title: Tvinga Flashens reservstatus med hjälp av mediekälllistan
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Tvinga Flashens reservstatus med hjälp av mediekälllistan{#forcing-the-flash-fallback-using-the-media-source-list}

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
