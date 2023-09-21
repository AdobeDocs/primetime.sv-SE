---
description: Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.
title: Vänta på ett giltigt tillstånd
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.

Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone rätt läge, kommer många spelarmetoder att generera `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att läget är förberett:

   När spelaren initieras väntar du tills webbläsarens TVSDK skickar `AdobePSDK.MediaPlayerStatusChangeEvent` händelse med `event.status` av `MediaPlayerStatus.PREPARED`.

   Om du vill kontrollera om det aktuella läget för MediaPlayer-objektet är åtminstone FÖRBEREDD.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
