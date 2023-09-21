---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Säker annonsinläsning över HTTPS {#secure-ad-loading-over-https}

Adobe Primetime erbjuder ett alternativ för att begära första anrop till Primetime-annonsservern och CRS-relaterade anrop via HTTPS.

Funktionen är inte aktiverad som standard. Använd följande för att aktivera säker annonsinläsning.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
