---
description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
title: Identifiera om innehållet är live eller VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# Identifiera om innehållet är live eller VOD {#identify-whether-the-content-is-live-or-vod}

Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).

1. Kontrollera att spelaren finns i åtminstone `PREPARED` tillstånd.
1. Avgör om `MediaPlayerItem` innehållet är live ( `true`) eller VOD ( `false`).

   ```java
   boolean isLive();
   ```
