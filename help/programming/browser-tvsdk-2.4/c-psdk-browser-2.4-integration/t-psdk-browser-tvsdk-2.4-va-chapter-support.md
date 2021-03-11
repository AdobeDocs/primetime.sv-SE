---
title: Stöd för implementeringskapitel
description: Stöd för implementeringskapitel
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# Implementera stöd för kapitel{#implement-chapter-support}

Ett kapitel definieras som tiden mellan varje annonsbrytning. Till exempel definieras tiden mellan en annonsbrytning före rullning och den första mittenrullen som det första kapitlet. Du kan definiera och spåra kapitel för videospårning i ett webbläsarbaserat TVSDK-baserat program med anpassade kapitel. Anpassade kapitel hanteras av programmet och baseras på CMS-data eller något annat sätt som programmet använder för att definiera kapitel.

1. Definiera och spåra anpassade kapitel.

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

