---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på ett giltigt tillstånd
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelaranvändargränssnittet. Innan du kan använda de flesta TVSDK-spelarmetoder måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har minst rätt status kommer många spelarmetoder att returnera `IllegalStateException`.

Den obligatoriska statusen är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att statusen är FÖRBEREDD:

   När spelaren initieras väntar du tills TVSDK anropar återanropet för händelsen `MediaPlayerStatusChangeEvent.STATUS_CHANGED` med statusen PREPARED.

   Om du vill kontrollera om den aktuella statusen för `MediaPlayer`-objektet är åtminstone FÖRBEREDD.

   ```
   function getstatus():String;
   ```
