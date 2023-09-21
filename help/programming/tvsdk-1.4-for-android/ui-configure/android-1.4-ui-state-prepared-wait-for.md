---
description: Med TVSDK kan du styra den grundläggande uppspelningsupplevelsen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.
title: Vänta på ett giltigt tillstånd
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningsupplevelsen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.

Innan du kan använda de flesta av TVSDK-spelarmetoderna måste spelaren vara i ett giltigt läge.
Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone rätt läge, kommer många spelarmetoder att generera `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.
