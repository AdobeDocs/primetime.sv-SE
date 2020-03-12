---
description: 'null'
seo-description: 'null'
seo-title: Säker annonsinläsning över HTTPS
title: Säker annonsinläsning över HTTPS
uuid: 0d680fef-a372-4157-a89b-d9f10003c768
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Säker annonsinläsning över HTTPS{#secure-ad-loading-over-https}

Adobe Primetime erbjuder ett alternativ för att begära första anrop till Primetime-annonsservern och CRS-relaterade anrop via HTTPS.

Funktionen är inte aktiverad som standard. Använd följande för att aktivera säker annonsinläsning.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

