---
description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
seo-description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
seo-title: Identifiera om innehållet är live eller VOD
title: Identifiera om innehållet är live eller VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Identifiera om innehållet är live eller VOD {#identify-whether-the-content-is-live-or-vod}

Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).

1. Kontrollera att spelaren är i åtminstone `PREPARED` läget.
1. Avgör om `MediaPlayerItem` innehållet är live ( `true`) eller VOD ( `false`).

   ```java
   boolean isLive();
   ```
