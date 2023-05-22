---
description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.

1. Se till att spelaren är i åtminstone tillståndet PREPARED.
1. Avgör om `MediaPlayerItem` innehållet är live (true) eller VOD (false).

   ```java
   boolean isLive();
   ```
