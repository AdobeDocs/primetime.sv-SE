---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.
title: DRM-händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

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
