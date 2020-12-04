---
description: Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.
seo-description: Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.
seo-title: DRM, Widewin
title: DRM, Widewin
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# DRM för Widewin {#widevine-drm}

Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.

Anropa följande `com.adobe.mediacore.drm.DRMManager` API innan uppspelningen startar:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argument:

* `drm` -  `"com.widevine.alpha"` för WideVM.

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

