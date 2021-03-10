---
description: I Adobe Primetime annonsbeslut kan ni rikta annonser på nyckelvärdepar.
title: Målinformation
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Målinformation{#targeting-information}

I Adobe Primetime annonsbeslut kan ni rikta annonser på nyckelvärdepar.

Så här skickar du nyckelvärdepar till Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

