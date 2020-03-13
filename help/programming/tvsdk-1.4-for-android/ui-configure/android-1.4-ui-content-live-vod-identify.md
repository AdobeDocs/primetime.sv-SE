---
description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
seo-description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
seo-title: Identifiera om innehållet är live eller VOD
title: Identifiera om innehållet är live eller VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.

1. Se till att spelaren är i åtminstone tillståndet PREPARED.
1. Bestäm om innehållet `MediaPlayerItem` är live (true) eller VOD (false).

   ```java
   boolean isLive();
   ```

