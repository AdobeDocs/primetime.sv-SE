---
description: Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.
title: DRM, Widewin
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
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

