---
title: Stöd för implementeringskapitel
description: Stöd för implementeringskapitel
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Implementera kapitelstöd {#implement-chapter-support}

Du kan definiera och spåra *anpassade* kapitel för videospårning i TVSDK-baserade program.

Anpassade kapitel hanteras av programmet och baseras på CMS-data eller på något annat sätt som programmet använder för att definiera kapitel.

>[!CAUTION]
>
>Standardkapitel stöds inte i 2.5 Android TVSDK.

1. Definiera och spåra anpassade kapitel.

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

