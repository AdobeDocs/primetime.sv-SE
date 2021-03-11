---
description: Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.
title: Implementera stöd för anpassade metadata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# Implementera stöd för anpassade metadata{#implement-custom-metadata-support}

Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.

Återanropsfunktioner anropas precis innan spårningsanropet görs, så att programmet kan bifoga metadata som är specifika för en annons eller ett kapitel.

1. Anropa återanropsfunktioner för innehåll, annonser och kapitel.

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```

