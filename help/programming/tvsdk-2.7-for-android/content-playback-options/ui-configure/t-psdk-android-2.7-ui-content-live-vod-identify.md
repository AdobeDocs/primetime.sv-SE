---
description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
title: Identifiera om innehållet är live eller VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Identifiera om innehållet är live eller VOD {#identify-whether-the-content-is-live-or-vod}

Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).

1. Kontrollera att spelaren är i minst `PREPARED`-läge.
1. Avgör om `MediaPlayerItem`-innehållet är live ( `true`) eller VOD ( `false`).

   ```java
   boolean isLive();
   ```
