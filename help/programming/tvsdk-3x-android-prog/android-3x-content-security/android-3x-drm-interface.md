---
description: Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en DRMHelper-klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.
seo-description: Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en DRMHelper-klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.
seo-title: Översikt över Primetime DRM-gränssnittet
title: Översikt över Primetime DRM-gränssnittet
uuid: 9e6f6ae6-7193-40fe-bc9d-d8de33705f5d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Översikt över Primetime DRM-gränssnittet {#primetime-drm-interface-overview}

Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en `DRMHelper` klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM ger ett skalbart och effektivt arbetsflöde för att implementera innehållsskydd i TVSDK-program. Du skyddar och hanterar rättigheterna till ditt videoinnehåll genom att skapa en licens för varje digital mediefil.

Mer information finns i DRM-exempelspelarkoden som ingår i TVSDK-paketet.

Här är de viktigaste API-elementen för att arbeta med DRM:

* En referens i mediespelaren till DRM-hanterarobjektet som implementerar DRM-undersystemet:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Detta API returnerar bara ett giltigt `DRMManager` objekt när `MediaPlayerEvent.DRM_METADATA` det har utlösts. Om du anropar `getDRMManager()` innan den här händelsen utlöses kan den returnera NULL.

* Klassen `DRMHelper` help, som är användbar när du implementerar DRM-arbetsflöden.
* En inläsningsmetod för metadata, som läser in DRM-metadata när de finns i en separat URL från mediet. `DRMHelper`

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* En `DRMHelper` metod för att kontrollera DRM-metadata och avgöra om autentisering krävs.

   ```java
   /** 
   * Return whether authentication is needed for the provided 
   * DRMMetadata. 
   * 
   * @param drmMetadata 
   * The desired DRMMetadata on which to check whether auth is needed. 
   * @return whether authentication is required for the provided metadata 
   */ 
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

* `DRMHelper` metod för autentisering.

   ```java
   /** 
   * Helper method to perform DRM authentication. 
   * 
   * @param drmManager 
   * the DRMManager, used to perform the authentication. 
   * @param drmMetadata 
   * the DRMMetadata, containing the DRM specific information. 
   * @param authenticationListener 
   * the listener, on which the user can be notified about the 
   * authentication process status. 
   * @param authUser 
   * the DRM username provider by the user. 
   * @param authPass 
   * the DRM password provided by the user. 
   */ 
   public static void performDrmAuthentication(final DRMManager drmManager,  
   final DRMMetadata drmMetadata,  
   final String authUser,  
   final String authPass,  
   final DRMAuthenticationListener authenticationListener);
   ```

* Händelser som meddelar ditt program om olika DRM-aktiviteter och -status.

Mer information om DRM finns i [DRM-dokumentationen](https://helpx.adobe.com/primetime/user-guide.html).
