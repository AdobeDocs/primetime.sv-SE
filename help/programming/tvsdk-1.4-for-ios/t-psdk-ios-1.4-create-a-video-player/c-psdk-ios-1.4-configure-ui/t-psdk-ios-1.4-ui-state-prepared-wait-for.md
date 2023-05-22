---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på ett giltigt tillstånd
exl-id: 150b37b8-c36d-4143-bead-ddc601bba6fe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd{#wait-for-a-valid-state}

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att `IllegalStateException`.

Nödvändig status är vanligtvis `PTMediaPlayerStatusReady`.
