---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Säker annonsinläsning över HTTPS{#secure-ad-loading-over-https}

Adobe Primetime erbjuder ett alternativ för att begära första samtal till Primetime-annonsservern och CRS-relaterade samtal via HTTPS.

Funktionen är inte aktiverad som standard. Använd följande för att aktivera säker annonsinläsning.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
