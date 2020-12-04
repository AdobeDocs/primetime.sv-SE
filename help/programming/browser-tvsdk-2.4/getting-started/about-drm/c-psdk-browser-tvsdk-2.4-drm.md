---
description: Du kan slutföra DRM-specifika arbetsflöden (Digital Rights Management).
seo-description: Du kan slutföra DRM-specifika arbetsflöden (Digital Rights Management).
seo-title: Digital Rights Management
title: Digital Rights Management
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Du kan slutföra DRM-specifika arbetsflöden (Digital Rights Management).

Du kan lyssna på händelsen `AdobePSDK.DRMMetadataInfoEvent` för att hantera DRM-arbetsflöden:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Lägg till Digital Rights Management {#add-digital-rights-management}

1. Lägg till `DRMMetadataInfoAvailableEvent` för att hämta `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementera avsnittet `onDRMMetadataInfoAvailable` ovanför raden i steg 1.

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. Skapa DRMManager i setupVideo-metoden.

   ```js
   var drmManager = player.drmManager;
   ```

1. Skapa skyddsdata för Widewin och PlayReady genom att kopiera följande exempel:

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. Lägg till skyddsdata i drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Ändra resurs-URL:en till en DASH-testström.

   >[!TIP]
   >
   >Se till att du uppdaterar resurstypen eftersom detta nu är DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Testa konfigurationen.