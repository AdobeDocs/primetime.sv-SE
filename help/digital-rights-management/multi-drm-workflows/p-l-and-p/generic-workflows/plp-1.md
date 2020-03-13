---
description: Du kan använda Adobes offlinepaketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.
seo-description: Du kan använda Adobes offlinepaketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.
seo-title: Primetime Packager / Cloud DRM / TVSDK
title: Primetime Packager / Cloud DRM / TVSDK
uuid: e54a0e4d-c8ea-46d4-b1b0-bed8a680f8f5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Du kan använda Adobes offlinepaketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.

Den här uppsättningen instruktioner förutsätter att du redan har konfigurerat ett ExpressPlay-administratörskonto: Snabbstart för [Primetime DRM Cloud](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Välj den infrastruktur som ska användas för att paketera ditt innehåll. Primetime Packager stöder både kommandorad- och konfigurationsbaserad paketering av innehåll som ska användas med DRM-DRM:erna FairPlay, Widewin och PlayReady. Följande format och kryptering stöds för närvarande i TVSDK (med mer i pipeline):

   * DASH (CENC) / PlayReady, Widewin - för HTML5
   * HLS/FairPlay, Access - för iOS

1. Välj ett KMS (Key Management System):

   * Använd ExpressPlays KMS ( [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/)); det här systemet hanterar dina innehållsnycklar via ExpressPlays RESTful API.

      eller...

   * Skapa en egen KMS. Skapa en databas med innehållsnycklar som kan väljas med innehålls-ID.

      I båda fallen hanterar KMS leveransen av innehållsnycklar, där varje nyckel har ett associerat innehålls-ID.

1. Paketera innehållet. Med Primetime Packager kan du paketera en del av innehållet för en viss DRM-lösning eller för flera DRM-lösningar.

   Följande exempelkommandon visar några exempel på paketering av innehåll för olika DRM-lösningar:

   * [Widewin med Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (genererar MPD-fil):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay med Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (Skapar en M3U8-fil):

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >Värdet `key_url` kopieras som i M3U8-filen.

1. Skapa en&quot;storefront server&quot;.

       Butiksservern måste hantera följande åtgärder:
   
   1. Kunden väljer innehåll. Den här implementeringen måste innehålla en slutpunkt där klienter kan begära en innehållstoken för ett visst innehålls-ID.
   1. Kundberättigande
   1. Licenstoken-begäranden (ExpressPlay) från klienten ( [ExpressPlay-licenstokenbegäran/svarsreferens](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Skapa en kund.

       Klienten bör innehålla ett anrop till din storefront-server. Adobe rekommenderar att kunden ringer butiken när användaren har valt visst innehåll och efter att användaren har autentiserats. Skicka sedan den token som returnerats från ExpressPlay till spelaren för att använda den för licensförfrågningar. Introduktioner till implementering av DRM-komponenten för dina spelare är här:
   
   * [Webbläsare-TVSDK för HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Med den aktuella licenstoken kan klienten nu hämta begärande-URL:en från token och göra licensbegäran till ExpressPlay och sedan spela upp det valda innehållet för användaren.
