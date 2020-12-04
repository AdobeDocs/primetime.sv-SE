---
description: Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.
seo-description: Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.
seo-title: Identifiera om innehållet är live eller VOD
title: Identifiera om innehållet är live eller VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.

1. Vänta tills Browser TVSDK utlöser en `AdobePSDK.PSDKEventType.STATUS_CHANGED`-händelse med `event.status` av `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Detta steg säkerställer att medieresursen har lästs in.

   >[!IMPORTANT]
   >
   >Om webbläsarens TVSDK inte är i minst `PREPARED`-läget, kommer ett försök att anropa följande metoder att resultera i `IllegalStateException`.

1. Läs `live` från gränssnittet `MediaPlayerItem`:

   ```js
   player.currentItem.live
   ```

