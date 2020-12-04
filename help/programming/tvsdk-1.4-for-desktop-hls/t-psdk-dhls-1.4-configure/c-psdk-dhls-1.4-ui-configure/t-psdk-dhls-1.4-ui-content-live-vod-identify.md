---
description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
seo-description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
seo-title: Identifiera om innehållet är live eller VOD
title: Identifiera om innehållet är live eller VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.

1. Kontrollera att spelaren har minst statusen INITIALIZED.
1. Avgör om `MediaPlayerItem`-innehållet är live (true) eller VOD (false).

   ```
   function get isLive():Boolean;
   ```

