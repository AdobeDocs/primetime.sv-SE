---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på en giltig status
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.

Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att visa `MediaPlayerException`.

Statusen som krävs är vanligtvis FÖRBEREDD. När detta inträffar sker callback-funktionen för `StatusChangeEventListener.onStatusChanged()` körs.

1. Bekräfta att statusen är `PREPARED`, kontrollera `MediaPlayer.MediaPlayerStatus`.
