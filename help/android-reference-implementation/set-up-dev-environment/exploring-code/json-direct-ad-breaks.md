---
title: JSON-objekt för direkta annonsbrytningar
description: Detaljerar JSON-objektet när typvärdet är direkt och brytningar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# JSON-objekt för direkta annonsbrytningar{#json-object-for-direct-ad-breaks}

Följande kodblock definierar JSON-objektet details när typvärdet är direkt annonsbrytning.

The `MetadataNode` returneras av `IFeedItemAdapter:getStreamMetadata()` innehåller en post med en typnyckel `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` och värdet för en strängbeteckning för JSON-objektvärdet med information nedan.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| Egenskap | Beskrivning |
|---|---|
| `tag` | En sträng som mappar till taggfältet i `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Anger starttiden för annonsbrytningen, mappar till tidsfältet i `com.adobe.mediacore.timeline.advertising.AdBreak`. Värdet 0 anger en annons före rullning. |
| `replace` | Anger varaktigheten för annonsbrytningen, mappar till `replaceDuration` fält i `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | En lista över annonser som ska spelas upp under den angivna annonsuppdelningen, mappar till `List<Ad>` fält i `com.adobe.mediacore.timeline.advertising.AdBreak`. |

Följande kodblock definierar JSON-objektet för arrayen med annonslista.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| Egenskap | Beskrivning |
|---|---|
| `url` | URL:en till annonsinnehållet mappas till URL-fältet i `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | Annonsens varaktighet, mappar till varaktighetsfältet i `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | En beskrivningssträng. |
