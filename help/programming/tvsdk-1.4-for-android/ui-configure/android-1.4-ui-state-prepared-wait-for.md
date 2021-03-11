---
description: Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.
title: Vänta på ett giltigt tillstånd
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Vänta på ett giltigt tillstånd {#wait-for-a-valid-state}

Med TVSDK kan du styra den grundläggande uppspelningen för live och on demand-video (VOD). TVSDK innehåller metoder och egenskaper för spelarinstansen som du kan använda för att konfigurera spelargränssnittet.

Innan du kan använda de flesta TVSDK-spelarmetoderna måste spelaren vara i ett giltigt läge.
Spelaren rör sig genom olika lägen. Om du väntar på att spelaren ska vara i rätt läge ser du till att medieresursen har lästs in. Om spelaren inte är i åtminstone det läge som krävs kommer många spelarmetoder att generera `IllegalStateException`.

Tillståndet som krävs är vanligtvis FÖRBEREDD.
