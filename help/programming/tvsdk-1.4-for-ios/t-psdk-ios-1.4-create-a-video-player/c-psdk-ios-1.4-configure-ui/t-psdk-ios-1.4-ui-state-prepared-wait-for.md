---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-title: Vänta på ett giltigt tillstånd
title: Vänta på ett giltigt tillstånd
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Vänta på ett giltigt tillstånd{#wait-for-a-valid-state}

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att returnera `IllegalStateException`.

Den obligatoriska statusen är vanligtvis `PTMediaPlayerStatusReady`.
