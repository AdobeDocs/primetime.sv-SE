---
description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.

1. Se till att spelaren är i åtminstone tillståndet PREPARED.
1. Avgör om `MediaPlayerItem`-innehållet är live (true) eller VOD (false).

   ```java
   boolean isLive();
   ```

