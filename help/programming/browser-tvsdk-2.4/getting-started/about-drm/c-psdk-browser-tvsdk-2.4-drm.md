---
description: Du kan slutföra DRM-specifika arbetsflöden (Digital Rights Management).
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
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