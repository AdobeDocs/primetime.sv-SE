---
description: Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.
title: DRM, Widewin
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
