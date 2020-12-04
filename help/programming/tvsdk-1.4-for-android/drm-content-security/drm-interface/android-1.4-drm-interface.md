---
description: Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad Primetime DRM-lösning.
seo-description: Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad Primetime DRM-lösning.
seo-title: Översikt över Primetime DRM-gränssnittet
title: Översikt över Primetime DRM-gränssnittet
uuid: 71479464-8356-4732-9774-da9f6084e6ad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Översikt {#primetime-drm-interface-overview}

Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad Primetime DRM-lösning.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Kontakta din Adobe-representant för att få den senaste informationen om tillgängliga DRM-lösningar från tredje part.

Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager. Exempelprogrammet som ingår i Android SDK innehåller en `DRMHelper`-klass som visar hur du gör vissa DRM-åtgärder enklare att implementera.

Primetime DRM ger ett skalbart och effektivt arbetsflöde för att implementera innehållsskydd i TVSDK-program. Du skyddar och hanterar rättigheterna till ditt videoinnehåll genom att skapa en licens för varje digital mediefil.

Se exempelkoden för DRM som ingår i TVSDK-paketet.

Detta är de viktigaste API-elementen för att arbeta med DRM:

* En referens i mediespelaren till DRM-hanterarobjektet som implementerar DRM-undersystemet:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Detta API returnerar ett giltigt `DRMManager`-objekt först efter att `MediaPlayerEvent.DRM_METADATA` har utlösts. Om du anropar `getDRMManager()` innan den här händelsen utlöses kan det returnera NULL.

* Hjälpklassen `DRMHelper`, som är användbar när du implementerar DRM-arbetsflöden.

   Du kan se `DRMHelper` i `ReferencePlayer`.

* En `DRMHelper`-metadatainläsarmetod som läser in DRM-metadata när den finns i en separat URL från mediet.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* En `DRMHelper`-metod för att kontrollera DRM-metadata för att avgöra om autentisering krävs.

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

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Ytterligare relevanta API-element:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Mer information om DRM finns i [Adobe Primetime DRM-dokumentationen](https://helpx.adobe.com/primetime/user-guide.html).
