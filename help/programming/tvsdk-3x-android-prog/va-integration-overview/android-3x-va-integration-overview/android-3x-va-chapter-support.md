---
description: 'null'
seo-description: 'null'
seo-title: Stöd för implementeringskapitel
title: Stöd för implementeringskapitel
uuid: 6e2c3994-d28b-489f-ae60-9b876125a871
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Stöd för implementeringskapitel {#implement-chapter-support}

Du kan definiera och spåra *anpassade* kapitel för videospårning i TVSDK-baserade program.

Anpassade kapitel hanteras av programmet och baseras på CMS-data eller på något annat sätt som programmet använder för att definiera kapitel.

>[!CAUTION]
>
>Standardkapitel stöds inte i 3.0 Android TVSDK.

Definiera och spåra anpassade kapitel.

```java
// First, enable chapter tracking by setting   
// enableChapterTracking to true: 
 
vaMetadata.enableChapterTracking(true); 
// For custom chapter definitions, provide  
// an array list of chapters through the metadata. 
// For example: 3 chapters of 60 second duration each 
 
List<VideoAnalyticsChapterData> chapters =  
  new ArrayList<VideoAnalyticsChapterData>(); 
 
Int chapterDuration = 60; 
for (var i = 0; i < 3; i++) { 
    VideoAnalyticsChapterData chapterData =  
      new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
    chapterData.setName("chapter_" + (i+1)); 
    chapters.add(chapterData); 
} 
 
vaMetadata.setChapters(chapters); 
```
