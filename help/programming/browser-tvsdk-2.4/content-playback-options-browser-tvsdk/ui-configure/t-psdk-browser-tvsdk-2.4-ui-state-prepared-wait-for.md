---
description: Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.
title: Vänta på ett giltigt tillstånd
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Innan du kan använda de flesta metoderna i webbläsarens TVSDK-spelare måste spelaren vara i ett giltigt läge.

Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone det läge som krävs, kommer många spelarmetoder att `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.

1. Så här bekräftar du att läget är förberett:

   När spelaren initieras väntar du tills webbläsarens TVSDK skickar `AdobePSDK.MediaPlayerStatusChangeEvent` händelse med `event.status` av `MediaPlayerStatus.PREPARED`.

   Om du vill kontrollera om det aktuella läget för MediaPlayer-objektet är åtminstone FÖRBEREDD.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
