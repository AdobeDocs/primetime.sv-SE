---
description: Om du vill få meddelanden om taggar i manifestet måste du implementera lämpliga händelseavlyssnare.
seo-description: Om du vill få meddelanden om taggar i manifestet måste du implementera lämpliga händelseavlyssnare.
seo-title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Lägg till avlyssnare för tidsbestämda metadataaviseringar {#add-listeners-for-timed-metadata-notifications}

Om du vill få meddelanden om taggar i manifestet måste du implementera lämpliga händelseavlyssnare.

Du kan övervaka tidsbestämda metadata genom att avlyssna `onTimedMetadata`, som meddelar programmet om relaterad aktivitet. Varje gång en unik prenumerationstagg identifieras under tolkningen av innehållet förbereder TVSDK ett nytt `TimedMetadata`-objekt och skickar den här händelsen. Objektet innehåller namnet på taggen som du prenumererar på, lokal tid i uppspelningen där taggen ska visas samt andra data.

Lyssna efter händelser.

```java
private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
    @Override 
    public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
        TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
 
        TimedMetadata.Type type = timedMetadata.getType(); 
        if (type.equals(TimedMetadata.Type.ID3)){ 
            Metadata metadata = timedMetadata.getMetadata(); 
            Set<String> keys = metadata.keySet(); 
            for (String key : keys) { 
                String value = metadata.getValue(key); 
            } 
        } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
            displayRanges(); 
        } 
    } 
}; 
```

ID3-metadata använder samma `onTimedMetadata`-avlyssnare för att ange om det finns en ID3-tagg. Detta bör dock inte skapa någon förvirring eftersom du kan använda egenskapen `TimedMetadata` `type` för att skilja mellan TAGG och ID3. Mer information om ID3-taggar finns i [ID3-taggar](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).