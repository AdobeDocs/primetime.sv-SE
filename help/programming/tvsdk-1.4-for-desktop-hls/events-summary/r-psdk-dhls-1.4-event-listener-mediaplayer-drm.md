---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.
title: DRM-händelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# DRM-händelser{#drm-events}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.

Om du vill få meddelanden om alla DRM-relaterade händelser avlyssnar du `DRMMetadataInfoEvent` för DRM-händelser med `MediaPlayer` -objekt.

| Händelse | Betydelse |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Nya DRM-metadata är tillgängliga. |
