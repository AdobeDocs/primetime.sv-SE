---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
exl-id: f9de1a2b-4eea-4028-83db-1b4021d1fbb7
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
