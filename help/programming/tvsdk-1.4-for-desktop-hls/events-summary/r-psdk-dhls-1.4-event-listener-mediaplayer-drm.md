---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.
seo-description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.
seo-title: DRM-händelser
title: DRM-händelser
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# DRM-händelser{#drm-events}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.

Om du vill få meddelanden om alla DRM-relaterade händelser lyssnar du efter DRM-händelser `DRMMetadataInfoEvent` med `MediaPlayer` objektet.

| Händelse | Betydelse |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Nya DRM-metadata är tillgängliga. |