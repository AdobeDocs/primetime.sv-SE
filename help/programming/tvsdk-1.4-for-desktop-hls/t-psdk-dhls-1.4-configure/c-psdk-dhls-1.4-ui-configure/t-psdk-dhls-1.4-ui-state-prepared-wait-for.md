---
description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-description: Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren ha en giltig status.
seo-title: Vänta på ett giltigt tillstånd
title: Vänta på ett giltigt tillstånd
uuid: 918ab021-3685-424a-b84e-683da0357724
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelaranvändargränssnittet. Innan du kan använda de flesta TVSDK-spelarmetoder måste spelaren ha en giltig status.

Spelaren rör sig genom olika statusar. Om du väntar på att spelaren ska ha rätt status ser du till att medieresursen har lästs in. Om spelaren inte har den status som krävs, kommer många spelarmetoder att generera `IllegalStateException`.

Den obligatoriska statusen är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att statusen är FÖRBEREDD:

   När spelaren initieras väntar du tills TVSDK anropar återanropet för `MediaPlayerStatusChangeEvent.STATUS_CHANGED` händelsen med statusen PREPARED.

   Om du vill kontrollera om objektets aktuella status är minst `MediaPlayer` FÖRBEREDD.

   ```
   function getstatus():String;
   ```
