---
description: Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.
title: Implementera stöd för anpassade metadata
exl-id: c7478578-7f49-4fd0-b381-c558888401aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementera stöd för anpassade metadata{#implement-custom-metadata-support}

Du kan tillhandahålla anpassade metadata för innehåll, annonser och kapitelspårningsanrop med hjälp av callback-funktioner.

Återanropsfunktioner anropas precis innan spårningsanropet görs, så att programmet kan bifoga metadata som är specifika för en annons eller ett kapitel.

Anropa återanropsfunktioner för innehåll, annonser och kapitel.

```
// Video Metadata Block 
    vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
    { 
        return @{ 
                 @"myvideoid": @"1234", 
                 @"mysdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Ad Metadata Block invoked on every ad start 
    vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
    { 
        return @{ 
                 @"myadid": @"ad-1234", 
                 @"myad-sdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Chapter Metadata Block invoked on every chapter start 
    vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
    { 
        return @{ 
                 @"mychapterid": @"chapter-1234", 
                 @"mychapter-sdkversion": [PTSDK apiVersion] 
                 }; 
    };
```
