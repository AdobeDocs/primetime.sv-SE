---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-title: Vänta på en giltig status
title: Vänta på en giltig status
uuid: 7a86b4cf-f7a0-4d90-9ff2-401640a395c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Vänta på en giltig status {#wait-for-a-valid-status}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att returnera `MediaPlayerException`.

Den obligatoriska statusen är vanligtvis FÖRBEREDD. När detta inträffar körs callback-rutinen för `StatusChangeEventListener.onStatusChanged()`.

Kontrollera `MediaPlayer.MediaPlayerStatus` för att bekräfta att statusen är `PREPARED`.