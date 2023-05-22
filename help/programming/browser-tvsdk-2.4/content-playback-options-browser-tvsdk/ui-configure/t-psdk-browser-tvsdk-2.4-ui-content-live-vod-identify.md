---
description: Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.

1. Vänta på att webbläsarens TVSDK ska aktivera en `AdobePSDK.PSDKEventType.STATUS_CHANGED` händelse med `event.status` av `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Detta steg säkerställer att medieresursen har lästs in.

   >[!IMPORTANT]
   >
   >Om webbläsarens TVSDK inte finns i åtminstone `PREPARED` tillstånd, försök att anropa följande metoder ger ett `IllegalStateException`.

1. Läs `live` från `MediaPlayerItem` gränssnitt:

   ```js
   player.currentItem.live
   ```
