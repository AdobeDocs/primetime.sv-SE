---
title: Stöd för implementeringskapitel
description: Stöd för implementeringskapitel
copied-description: true
exl-id: f86af555-4eba-4bc8-a323-41f65f23f4cc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Stöd för implementeringskapitel {#implement-chapter-support}

Du kan definiera och spåra kapitel för videospårning i ett TVSDK-baserat program på följande sätt:

* Standardkapitel, som hanteras internt av TVSDK.

   Ett kapitel definieras som tiden mellan varje annonsbrytning. Till exempel definieras tiden mellan en annonsbrytning före rullning och den första mittenrullen som det första kapitlet.
* Anpassade kapitel, som hanteras av programmet och som baseras på CMS-data eller något annat sätt som programmet använder för att definiera kapitel.

1. Definiera och spåra standardkapitel eller anpassade kapitel.

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
