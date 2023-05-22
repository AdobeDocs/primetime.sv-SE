---
description: Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod
title: Uppgradera från 2.5.x Lazy Ad Resolving till 3.0.0 Lazy Ad Resolving (API/Workflow changes)
exl-id: 403ccb25-99a9-4545-9d17-3b71583bc6d8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Uppgradera från 2.5.x Lazy Ad Resolving to 3.x Lazy Ad Resolving (API/Workflow changes):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod:

**Placement.Type getPlacementType()**

Den här metoden returnerar placeringstypen Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL eller Placement.Type.POST_ROLL. Om en annonsbrytning är olöst visas `getDuration()`-metoden i TimelineMarker-gränssnittet returnerar 0.

>[!NOTE]
>
>Det här gränssnittet typkonverteras inte alltid till typen com.mediacore.timeline.advertising.AdBreakTimelineItem om den ännu inte har lösts. Den kan kastas om `getDuration()` TimelineMarker-metoden är större än 0.

**Händelseändringar:**

`kEventAdResolutionComplete` är nu avskriven och aktiveras nu omedelbart efter att spelaren har förberetts. Program som tidigare bara lyssnade på den här händelsen för att rita rensningsfältet bör ändra detta till att lyssna efter `kEventTimelineUpdated` endast. När de enskilda annonsbrytningarna är klara finns en ny `kEventTimelineUpdated` -händelsen skickas.
