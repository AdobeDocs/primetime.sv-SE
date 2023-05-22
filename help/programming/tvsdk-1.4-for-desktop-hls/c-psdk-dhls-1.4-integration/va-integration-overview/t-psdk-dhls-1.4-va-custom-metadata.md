---
description: Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.
title: Implementera stöd för anpassade metadata
exl-id: 56580338-5104-4121-b441-5d92ba6f4610
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementera stöd för anpassade metadata{#implement-custom-metadata-support}

Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.

Återanropsfunktioner anropas precis innan spårningsanropet görs, så att programmet kan bifoga metadata som är specifika för en annons eller ett kapitel.

1. Anropa återanropsfunktioner för innehåll, annonser och kapitel.

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```
