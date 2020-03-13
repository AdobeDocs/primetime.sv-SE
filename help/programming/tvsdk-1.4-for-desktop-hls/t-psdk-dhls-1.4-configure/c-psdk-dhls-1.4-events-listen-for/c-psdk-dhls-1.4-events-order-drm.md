---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.
seo-description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.
seo-title: DRM-händelser
title: DRM-händelser
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# DRM-händelser{#drm-events}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.

Om du vill få meddelanden om alla DRM-relaterade händelser lyssnar du efter följande:

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

I följande exempel visas ett typiskt förlopp:

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

