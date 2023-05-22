---
description: I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.
title: Identifiera om innehållet är live eller VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identifiera om innehållet är live eller VOD{#identify-whether-the-content-is-live-or-vod}

I vissa fall måste du veta om medieinnehållet är direktsänt eller VOD.

1. Kontrollera att spelaren har minst statusen INITIALIZED.
1. Avgör om `MediaPlayerItem` innehållet är live (true) eller VOD (false).

   ```
   function get isLive():Boolean;
   ```
