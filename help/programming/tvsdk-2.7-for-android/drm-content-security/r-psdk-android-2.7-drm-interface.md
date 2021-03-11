---
description: Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en DRMHelper-klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.
title: Översikt över Primetime DRM-gränssnittet
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Översikt över gränssnittet för Primetime DRM {#primetime-drm-interface-overview}

Det viktigaste klientelementet i Primetime DRM-lösningen är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller också en DRMHelper-klass som kan användas för att göra vissa DRM-åtgärder enklare att implementera.

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
   >Detta API returnerar ett giltigt `DRMManager`-objekt först efter att `MediaPlayerEvent.DRM_METADATA` har utlösts. Om du anropar `getDRMManager()` innan den här händelsen utlöses kan det returnera NULL.

* Hjälpklassen `DRMHelper`, som är användbar när du implementerar DRM-arbetsflöden.
* En `DRMHelper`-metadatainläsarmetod som läser in DRM-metadata när den finns i en separat URL från mediet.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* En `DRMHelper`-metod för att kontrollera DRM-metadata och avgöra om autentisering krävs.

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

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Mer information om DRM finns i [DRM-dokumentationen](https://helpx.adobe.com/primetime/user-guide.html).
