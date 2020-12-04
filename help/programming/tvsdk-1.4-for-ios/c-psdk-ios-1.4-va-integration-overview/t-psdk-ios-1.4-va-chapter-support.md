---
description: 'null'
seo-description: 'null'
seo-title: Stöd för implementeringskapitel
title: Stöd för implementeringskapitel
uuid: 4224cd2e-1e16-4040-972b-92c91506408f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '97'
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

