---
description: Du kanske behöver veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
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

