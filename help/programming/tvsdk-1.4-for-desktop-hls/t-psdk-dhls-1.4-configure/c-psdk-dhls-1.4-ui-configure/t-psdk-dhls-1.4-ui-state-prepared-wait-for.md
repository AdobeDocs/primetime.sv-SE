---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
title: Vänta på ett giltigt tillstånd
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningsupplevelsen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelaranvändargränssnittet. Innan du kan använda de flesta TVSDK-spelarmetoder måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har den status som krävs returneras många spelarmetoder `IllegalStateException`.

Statusen som krävs är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att statusen är FÖRBEREDD:

   När spelaren initieras väntar du tills TVSDK anropar återanropet för `MediaPlayerStatusChangeEvent.STATUS_CHANGED` händelse med PREPARED-status.

   Kontrollera om aktuell status för `MediaPlayer` -objektet är åtminstone PREPARED.

   ```
   function getstatus():String;
   ```
