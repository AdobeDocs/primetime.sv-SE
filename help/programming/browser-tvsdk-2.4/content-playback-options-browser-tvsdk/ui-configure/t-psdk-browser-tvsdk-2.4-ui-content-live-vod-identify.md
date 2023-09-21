---
description: Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
