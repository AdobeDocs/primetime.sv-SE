---
description: Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad lösning.
title: DRM, Widewin
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# DRM, Widewin {#widevine-drm}

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

Ring följande `com.adobe.mediacore.drm.DRMManager` API innan MediaPlayer-resursen läses in:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argument {#arguments-license-server}

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

## Ange anpassad återanrop {#custom-callback}

Ring följande `com.adobe.mediacore.drm.DRMManager` API innan MediaPlayer-resursen läses in.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argument {#arguments-custom-callback}

* `callback` - anpassad implementering av MediaDrmCallback som ska användas i stället för standardversionen `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Mer information finns i [Android TVSDK 3.11 API-dokumentation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Hämta PSSH-ruta för den aktuella inlästa MediaPlayer-resursen {#pssh-box-mediaplayer-resoource}

Ring följande `com.adobe.mediacore.drm.DRMManager` API, helst i anpassad återanropsimplementering.

```java
public static byte[] getPSSH()
```

API returnerar den systemspecifika rubrikruta för skydd som är associerad med den inlästa Widewin-medieresursen.

Det finns en giltig ruta med kort varaktighet (mellan skapande av DRM-instans och inläsning av nycklar). `MediaDrmCallback callback executeKeyRequest()` kan använda den för att anpassa hämtning av licensnycklar.

>[!NOTE]
>
> `getPSSH()` API stöds endast med en spelarinstans. Flera spelare eller Instant On-funktionen ska initieras seriellt för att få rätt ruta.
