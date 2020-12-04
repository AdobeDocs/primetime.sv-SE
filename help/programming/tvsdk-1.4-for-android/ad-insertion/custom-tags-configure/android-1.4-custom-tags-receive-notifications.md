---
description: Implementera lämpliga händelseavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-description: Implementera lämpliga händelseavlyssnare om du vill få meddelanden om taggar i manifestet.
seo-title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
title: Lägg till avlyssnare för tidsbestämda metadataaviseringar
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Lägg till avlyssnare för tidsbestämda metadataaviseringar {#add-listeners-for-timed-metadata-notifications}

Implementera lämpliga händelseavlyssnare om du vill få meddelanden om taggar i manifestet.

Du kan övervaka tidsbestämda metadata genom att avlyssna följande händelser som meddelar programmet om relaterade aktiviteter:

* `onTimedMetadata`: Varje gång en unik prenumerationstagg identifieras under tolkningen av innehållet förbereder TVSDK ett nytt  `TimedMetadata` objekt och skickar den här händelsen.

   Objektet innehåller namnet på taggen som du prenumererar på, lokal tid i uppspelningen där taggen ska visas samt andra data.

   Lyssna efter händelser.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
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
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

ID3-metadata använder samma onTimedMetadata-avlyssnare för att ange om det finns en ID3-tagg. Detta bör dock inte skapa någon förvirring eftersom du kan använda ett `TimedMetadata`-objekts `type`-egenskap för att skilja mellan TAG och ID3. Mer information om ID3-taggar finns i [ID3-taggar](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
