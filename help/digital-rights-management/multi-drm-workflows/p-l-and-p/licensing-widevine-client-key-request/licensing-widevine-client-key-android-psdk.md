---
description: Klientkoden skickar data till ett Android-API.
seo-description: Klientkoden skickar data till ett Android-API.
seo-title: Arbetsflöde för nyckelbegäran i Android PSDK
title: Arbetsflöde för nyckelbegäran i Android PSDK
uuid: 575163de-0f96-434d-a3ff-7e114caf72de
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Arbetsflöde för nyckelbegäran i Android PSDK{#key-request-workflow-on-android-psdk}

Klientkoden skickar data till ett Android-API.

På Android ska din klientkod skicka in licensserverns URL och tillhörande licenshämtningsdata med följande API:

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

När du har anropat detta API kan koden starta innehållsuppspelningen på det vanliga sättet. Om du använder Expresdisplay kan du antingen skicka token som en del av licensserverns URL eller som en request-egenskap och ta bort token från licensserverns URL.

Vissa Android-enheter har stöd för både Widewin och PlayReady. På sådana enheter kanske kunden vill tvinga PSDK att dekryptera innehållet med en viss DRM om innehållet har flera DRM-huvuden. Detta kan du göra genom att anropa följande API före uppspelning:

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```

