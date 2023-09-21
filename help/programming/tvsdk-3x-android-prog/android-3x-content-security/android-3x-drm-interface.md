---
description: Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en DRMHelper-klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.
title: Översikt över Primetime DRM-gränssnittet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Översikt över Primetime DRM-gränssnittet {#primetime-drm-interface-overview}

Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller även en `DRMHelper` klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.

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
  >Detta API returnerar en giltig `DRMManager` endast efter `MediaPlayerEvent.DRM_METADATA` har fått sparken. Om du ringer `getDRMManager()` innan den här händelsen utlöses kan den returnera NULL.

* The `DRMHelper` hjälpklass, vilket är användbart när du implementerar DRM-arbetsflöden.
* A `DRMHelper` Metoden för inläsning av metadata, som läser in DRM-metadata när den finns i en separat URL från mediet.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` metod för att kontrollera DRM-metadata och avgöra om autentisering krävs.

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

Mer information om DRM finns i [DRM-dokumentation](https://helpx.adobe.com/primetime/user-guide.html).
