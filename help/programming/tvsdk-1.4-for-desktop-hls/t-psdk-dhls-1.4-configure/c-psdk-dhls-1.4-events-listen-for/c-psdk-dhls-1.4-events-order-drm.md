---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga. Spelaren kan implementera åtgärder som svar på dessa händelser.
title: DRM-händelser
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
