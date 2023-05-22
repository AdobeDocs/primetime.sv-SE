---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på en giltig status
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Vänta på en giltig status {#wait-for-a-valid-status}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att `MediaPlayerException`.

Den obligatoriska statusen är vanligtvis FÖRBEREDD. När detta inträffar sker callback-funktionen för `StatusChangeEventListener.onStatusChanged()` körs.

Bekräfta att statusen är `PREPARED`, kontrollera `MediaPlayer.MediaPlayerStatus`.
