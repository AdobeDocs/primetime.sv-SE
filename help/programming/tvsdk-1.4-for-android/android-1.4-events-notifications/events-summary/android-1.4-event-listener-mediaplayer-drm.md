---
description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.
seo-description: TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.
seo-title: DRM-händelser
title: DRM-händelser
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# DRM-händelser{#drm-events}

TVSDK skickar DRM-händelser (Digital Rights Management) som svar på DRM-relaterade åtgärder som när nya DRM-metadata blir tillgängliga.

Om du vill få meddelanden om alla DRM-relaterade händelser registrerar du en implementering av `MediaPlayer.DRMEventListener` som innehåller följande återanrop.

| Händelse | Betydelse |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Nya DRM-metadata är tillgängliga. |

