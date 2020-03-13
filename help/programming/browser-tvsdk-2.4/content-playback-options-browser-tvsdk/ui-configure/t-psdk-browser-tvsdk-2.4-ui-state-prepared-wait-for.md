---
description: Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.
seo-description: Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.
seo-title: Vänta på ett giltigt tillstånd
title: Vänta på ett giltigt tillstånd
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.

Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone det läge som krävs, kommer många spelarmetoder att aktiveras `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att läget är förberett:

   När spelaren initieras väntar du på att webbläsarens TVSDK ska skicka `AdobePSDK.MediaPlayerStatusChangeEvent` händelsen med ett `event.status` av `MediaPlayerStatus.PREPARED`.

   Om du vill kontrollera om det aktuella läget för MediaPlayer-objektet är åtminstone FÖRBEREDD.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

