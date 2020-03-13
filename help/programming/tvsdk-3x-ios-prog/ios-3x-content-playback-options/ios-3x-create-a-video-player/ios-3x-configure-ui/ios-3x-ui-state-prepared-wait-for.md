---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-title: Vänta på ett giltigt tillstånd
title: Vänta på ett giltigt tillstånd
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst den status som krävs, kommer många spelarmetoder att generera `IllegalStateException`.

Den obligatoriska statusen är vanligtvis `PTMediaPlayerStatusReady`.