---
description: Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod
title: Uppgradera från 2.5.x Lazy Ad Resolving till 3.0.0 Lazy Ad Resolving (API/Workflow changes)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
