---
title: JSON-objekt för anpassade annonsmarkörer
description: JSON-objekt för anpassade annonsmarkörer
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# JSON-objekt för anpassade annonsmarkörer {#json-object-for-custom-ad-markers}

Kodblocket nedan definierar JSON-objektet &quot;details&quot; när typen är anpassade annonsmarkörer.

MetadataNode som returneras av IFeedItemAdapter:getStreamMetadata() innehåller 2 poster:
1. en post med en typnyckel `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` och värdet för en instans av MetadataNode som returneras av `TimeRangeCollection.toMetadata()`.
1. Den andra posten har en typnyckel `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` med värdet för *adjust-seek-position* attribut nedan.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| Egenskap | Beskrivning |
|---|---|
| adjust-seek-position | true eller false, används för att ange värdet för nyckeln com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED i MetadataNode. |
| tidsintervall | En array med JSON-objekt som anger tidsintervallet för varje annonsmarkör. Varje JSON-objektpost mappar till en instans av com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Värde i ms som anger annonsmarkörens starttid. |
| time-ranges.end | Värde i ms som anger sluttiden för annonsmarkören. |

Mer information om hur anpassade annonsmarkörer fungerar finns i TVSDK-dokumentationen.
