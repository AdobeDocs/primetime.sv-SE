---
description: Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.
title: Vänta på ett giltigt tillstånd
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.

Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone det läge som krävs kommer många spelarmetoder att generera `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att läget är förberett:

   När spelaren initieras väntar du tills webbläsarens TVSDK skickar händelsen `AdobePSDK.MediaPlayerStatusChangeEvent` med `event.status` av `MediaPlayerStatus.PREPARED`.

   Om du vill kontrollera om det aktuella läget för MediaPlayer-objektet är åtminstone FÖRBEREDD.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

