---
description: Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.
title: DRM, Widewin
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# DRM, Widewin {#widevine-drm}

Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.

Ring följande `com.adobe.mediacore.drm.DRMManager` API innan uppspelningen börjar:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argument:

* `drm` - `"com.widevine.alpha"` för WideVM.

* `licenseServerURL` - URL:en för den Wideglobal licensserver som tar emot licensbegäranden.
* `requestProperties` - Innehåller extra rubriker som ska inkluderas i begäran om utgående licens.

Om du till exempel använder innehåll som paketerats för Expresplay DRM ska du använda följande kod innan du spelar upp:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
