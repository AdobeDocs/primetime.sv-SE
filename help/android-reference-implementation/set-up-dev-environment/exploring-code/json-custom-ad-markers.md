---
title: JSON-objekt för anpassade annonsmarkörer
description: JSON-objekt för anpassade annonsmarkörer
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
