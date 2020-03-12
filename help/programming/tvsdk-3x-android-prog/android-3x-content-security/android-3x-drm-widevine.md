---
description: Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade lösning.
seo-description: Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade lösning.
seo-title: DRM, Widewin
title: DRM, Widewin
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# DRM, Widewin {#widevine-drm}

Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade lösning.

Kontakta din Adobe-representant för att få den senaste informationen om tillgängliga DRM-lösningar från tredje part.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Du kan använda det inbyggda Android-DRM för Widewin med DASH-strömmar.

Anropa följande `com.adobe.mediacore.drm.DRMManager` API innan uppspelningen startar:

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
