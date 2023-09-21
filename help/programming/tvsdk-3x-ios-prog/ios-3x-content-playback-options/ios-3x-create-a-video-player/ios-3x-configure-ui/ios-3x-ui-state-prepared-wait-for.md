---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på ett giltigt tillstånd
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att visa `IllegalStateException`.

Nödvändig status är vanligtvis `PTMediaPlayerStatusReady`.
