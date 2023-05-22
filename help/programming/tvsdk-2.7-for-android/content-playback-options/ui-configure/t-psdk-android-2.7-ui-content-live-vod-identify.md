---
description: Du kan behöva veta om medieinnehållet är live eller on demand-video (VOD).
title: Identifiera om innehållet är live eller VOD
exl-id: 756d4f04-d354-4194-80c9-c2ea6198a566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
