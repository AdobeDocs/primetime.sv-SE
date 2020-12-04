---
seo-title: JSON-objekt för direkta annonsbrytningar
title: JSON-objekt för direkta annonsbrytningar
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: Detaljerar JSON-objektet när typvärdet är direkt och brytningar
seo-description: Detaljerar JSON-objektet när typvärdet är direkt och brytningar
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# JSON-objekt för direkta annonsbrytningar{#json-object-for-direct-ad-breaks}

Följande kodblock definierar JSON-objektet details när typvärdet är direkt annonsbrytning.

`MetadataNode` som returneras av `IFeedItemAdapter:getStreamMetadata()` innehåller en post med nyckeln av typen `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` och värdet för en strängbeteckning för JSON-objektvärdet med information nedan.

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
| `replace` | Anger varaktigheten för annonsbrytningen, mappar till fältet `replaceDuration` i `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | En lista över annonser som ska spelas upp under den angivna annonsuppdelningen mappas till fältet `List<Ad>` i `com.adobe.mediacore.timeline.advertising.AdBreak`. |

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

