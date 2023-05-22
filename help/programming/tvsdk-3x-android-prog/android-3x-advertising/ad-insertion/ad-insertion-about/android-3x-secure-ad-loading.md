---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
exl-id: 752d9a35-2faa-4953-8357-e2aff445d3c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Säker annonsinläsning över HTTPS {#secure-ad-loading-over-https}

Adobe Primetime erbjuder ett alternativ för att begära första samtal till Primetime-annonsservern och CRS-relaterade samtal via HTTPS.

Funktionen är inte aktiverad som standard. Använd följande för att aktivera säker annonsinläsning.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
