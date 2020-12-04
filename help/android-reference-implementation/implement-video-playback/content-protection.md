---
description: Primetime-spelaren stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Detta innebär att ditt program måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp.
seo-description: Primetime-spelaren stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Detta innebär att ditt program måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp.
seo-title: Skydd av DRM-innehåll
title: Skydd av DRM-innehåll
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Skydd av DRM-innehåll {#drm-content-protection}

Primetime-spelaren stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Detta innebär att ditt program måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp.

Om du vill aktivera detta tillhandahåller TVSDK DRM-hanteraren för autentisering. Referensimplementeringen innehåller ett exempel på följande arbetsflöden:

* Så här läser du in och spelar upp HLS-strömmar med åtkomstmaterialskydd, optimerat för låga felnivåer och snabb start.
* Så här läser du in och spelar upp HLS-strömmar med AES128-innehållsskydd.
* Så här läser du in och spelar upp HLS-strömmar med skydd av PHLS-innehåll, optimerat för låg felfrekvens och snabb start.

Allt DRM-skyddat innehåll hanteras automatiskt av de DRM-bibliotek som är inbyggda i TVSDK. Du kan dock visa felhantering, optimering av enhetspersonalisering och licensköp med hjälp av API-återanrop för TVSDK.

## Lägg till innehållsskydd i spelaren {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Du kan lägga till innehållsskydd till spelaren genom att skapa en uppspelningshanterare eller genom att använda hanterarfabriken.

Så här skapar du en innehållshanterare:

* Initiera DRM-systemet.

   I följande kodexempel visas anropet `loadDRMServices` i funktionen `onCreate()` för att säkerställa att initieringen som krävs för DRM-systemet initieras innan uppspelningen startar.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Läs in DRM-licenserna i förväg.

   I följande kodexempel visas inläsningen av `VideoItems` när innehållslistan har lästs in. Detta resulterar i att DRM-licenserna hämtas från licensservern och cachas lokalt, så att innehållet läses in med minimal fördröjning när uppspelningen startar.

   ```java
   DrmManager.preLoadDrmLicenses(item.getUrl(),  
     new MediaPlayerItemLoader.LoaderListener() { 
   
       @Override 
       public void onLoadComplete(MediaPlayerItem item) { 
           Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
       } 
   
       @Override 
       public void onError(MediaErrorCode errorCode, String s) { 
           Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
       } 
   } 
   ```

   >[!NOTE]
   >
   >Du kan ställa in Preache DRM-licenser på ON i användargränssnittet för inställningar för att köra preache-DRM-licenser när du läser in innehåll. Det bästa sättet är dock att förhandsladda en viss post i stället för att alla licenser i katalogen lagras i förväg.
   >
   >![](assets/precache-drm-licenses.jpg)

* Om du vill använda `ManagerFactory` för att implementera DRM-felhantering måste följande kodrad finnas i filen [!DNL PlayerFragment.java]:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Relaterad API-dokumentation**

* [Klassen DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)