---
title: Stöd för implementeringskapitel
description: Stöd för implementeringskapitel
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Implementera stöd för kapitel{#implement-chapter-support}

Du kan definiera och spåra kapitel för videospårning i ett TVSDK-baserat program på följande sätt:

* Standardkapitel, som hanteras internt av TVSDK.

   Ett kapitel definieras som tiden mellan varje annonsbrytning. Till exempel definieras tiden mellan en annonsbrytning före rullning och den första mittenrullen som det första kapitlet.
* Anpassade kapitel, som hanteras av programmet och som baseras på CMS-data eller något annat sätt som programmet använder för att definiera kapitel.

   Definiera och spåra standardkapitel eller anpassade kapitel.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```

