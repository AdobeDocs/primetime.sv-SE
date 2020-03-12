---
description: I Adobe Primetimes annonsbeslut kan ni rikta annonser på nyckelvärdepar.
seo-description: I Adobe Primetimes annonsbeslut kan ni rikta annonser på nyckelvärdepar.
seo-title: Målinformation
title: Målinformation
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Målinformation{#targeting-information}

I Adobe Primetimes annonsbeslut kan ni rikta annonser på nyckelvärdepar.

Så här skickar du nyckelvärdepar till Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

