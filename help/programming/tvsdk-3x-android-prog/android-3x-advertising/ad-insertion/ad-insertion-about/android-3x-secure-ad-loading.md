---
description: 'null'
seo-description: 'null'
seo-title: Säker annonsinläsning över HTTPS
title: Säker annonsinläsning över HTTPS
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Säker annons som läses in via HTTPS {#secure-ad-loading-over-https}

Adobe Primetime erbjuder ett alternativ för att begära första samtal till Primetime-annonsservern och CRS-relaterade samtal via HTTPS.

Funktionen är inte aktiverad som standard. Använd följande för att aktivera säker annonsinläsning.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
