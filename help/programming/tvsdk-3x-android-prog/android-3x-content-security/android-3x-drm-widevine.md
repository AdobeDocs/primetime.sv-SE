---
description: Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad lösning.
seo-description: Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad lösning.
seo-title: DRM, Widewin
title: DRM, Widewin
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: 0271af21b74e80455ddb2c53571cd75f3a0f56ba
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# DRM för Widewin {#widevine-drm}

Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad lösning.

Kontakta din Adobe-representant för att få den senaste informationen om tillgängliga DRM-lösningar från tredje part.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Du kan använda Androids inbyggda Widewin DRM med HLS CMAF-strömmar.

>[!NOTE]
>
> Widewin CENC CTR-schemat kräver minst Android version 4.4 (API-nivå 19).
>
> Bredvid CBCS-schema kräver minst Android version 7.1 (API-nivå 25).

## Ange licensserverinformation {#license-server-details}

Anropa följande `com.adobe.mediacore.drm.DRMManager` API innan du läser in MediaPlayer-resursen:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argument {#arguments-license-server}

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

## Ange anpassad återanrop {#custom-callback}

Anropa följande `com.adobe.mediacore.drm.DRMManager`-API innan du läser in MediaPlayer-resursen.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argument {#arguments-custom-callback}

* `callback` - anpassad implementering av MediaDrmCallback som ska användas i stället för standardinställningen  `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Mer information finns i [Android TVSDK 3.11 API-dokumentation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Hämta PSSH-ruta för den aktuella inlästa MediaPlayer-resursen {#pssh-box-mediaplayer-resoource}

Anropa följande `com.adobe.mediacore.drm.DRMManager` API, helst i anpassad återanropsimplementering.

```java
public static byte[] getPSSH()
```

API returnerar den systemspecifika rubrikruta för skydd som är associerad med den inlästa Widewin-medieresursen.

Det finns en giltig ruta med kort varaktighet (mellan skapande av DRM-instans och inläsning av nycklar). `MediaDrmCallback callback executeKeyRequest()` kan använda den för att anpassa hämtning av licensnycklar.

>[!NOTE]
>
> `getPSSH()` API stöds endast med en spelarinstans. Flera spelare eller Instant On-funktionen ska initieras seriellt för att få rätt ruta.
