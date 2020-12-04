---
description: Du kan använda flera innehållslösare för att hantera olika tidslinjeåtgärder.
seo-description: Du kan använda flera innehållslösare för att hantera olika tidslinjeåtgärder.
seo-title: Innehållslösningar för borttagning/ersättning av annonser
title: Innehållslösningar för borttagning/ersättning av annonser
uuid: d43d54be-e04a-49dd-a695-e4e8f981ccb4
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# Innehållslösningar för borttagning/ersättning av annonser {#content-resolvers-for-ad-deletion-replacement}

Du kan använda flera innehållslösare för att hantera olika tidslinjeåtgärder.

```java
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
    List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
    MediaPlayerItemConfig itemConfig = item.getConfig(); 
    if(itemConfig) { 
        CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
        if (customRanges) { 
            List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
 
            if (timeRanges && timeRanges.size() > 0) { 
                //CustomRangeResolver is activated by the presence of CustomRanges 
                resolvers.add(new CustomRangeResolver()); 
            } 
        } 
        AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
        if (metadata) { 
            if (metadata instanceOf AuditudeSettings)  
            resolvers.add(new AuditudeResolver(getContext());                                      
        } 
    } 
    //Add your custom resolver if any 
    resolvers.add(MyOpportunityGenerator(item)); 
    return resolvers; 
} 
```
