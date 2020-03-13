---
description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
seo-description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
seo-title: Identifiera om innehållet är live eller VOD
title: Identifiera om innehållet är live eller VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Identifiera om innehållet är live eller VOD {#identify-whether-the-content-is-live-or-vod}

Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).

1. Kontrollera att spelaren är i åtminstone `PREPARED` läget.
1. Avgör om `MediaPlayerItem` innehållet är live ( `true`) eller VOD ( `false`).

   ```java
   boolean isLive();
   ```
