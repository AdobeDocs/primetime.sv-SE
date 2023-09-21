---
title: Stöd för implementeringskapitel
description: Stöd för implementeringskapitel
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Stöd för implementeringskapitel {#implement-chapter-support}

Du kan definiera och spåra kapitel för videospårning i ett TVSDK-baserat program på följande sätt:

* Standardkapitel, som hanteras internt av TVSDK.

  Ett kapitel definieras som tiden mellan varje annonsbrytning. Till exempel definieras tiden mellan en annonsbrytning före rullning och den första mittenrullen som det första kapitlet.
* Anpassade kapitel, som hanteras av programmet och som baseras på CMS-data eller något annat sätt som programmet använder för att definiera kapitel.

  Definiera och spåra standardkapitel eller anpassade kapitel.

  ```
  // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
  
      vaMetadata.enableChapterTracking = true; 
  
  // For custom chapter definitions, provide an array of chapters through the metadata:  
  // For example: 3 chapters of 60 second duration each 
  
      var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
      var chapterDuration:int = 60; 
      for (var i:int = 0; i < 3; i++) { 
          var chapterData:VideoAnalyticsChapterData =  
            new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
          chapterData.name = "chapter_%d" + (i+1); 
  
          chapters.push(chapterData); 
      } 
  
      vaMetadata.chapters = chapters; 
  
  // For default chapters, the application must not set custom chapters on the tracking metadata  
  // and simply enable chapters to be tracked by setting the boolean value as defined above. 
  ```
