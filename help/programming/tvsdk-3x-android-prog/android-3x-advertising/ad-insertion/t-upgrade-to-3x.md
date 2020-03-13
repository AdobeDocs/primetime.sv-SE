---
description: 'Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod '
seo-description: 'Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod '
seo-title: 'Uppgradera från 2.5.x Lazy Ad Resolving till 3.0.0 Lazy Ad Resolving (API/Workflow changes) '
title: 'Uppgradera från 2.5.x Lazy Ad Resolving till 3.0.0 Lazy Ad Resolving (API/Workflow changes) '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Uppgradera från 2.5.x Lazy Ad Resolving to 3.x Lazy Ad Resolving (API/Workflow changes):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod:

**Placement.Type getPlacementType()**

Den här metoden returnerar placeringstypen Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL eller Placement.Type.POST_ROLL. Om en annonsbrytning inte löses returnerar `getDuration()`metoden 0 i TimelineMarker-gränssnittet.

>[!NOTE]
>
>Det här gränssnittet typkonverteras inte alltid till typen com.mediacore.timeline.advertising.AdBreakTimelineItem om den ännu inte har lösts. Den kan kastas om metoden för `getDuration()` TimelineMarker är större än 0.

**Händelseändringar:**

`kEventAdResolutionComplete` är nu avskriven och aktiveras nu omedelbart efter att spelaren har förberetts. Program som tidigare bara lyssnade på den här händelsen för att rita rensningsfältet bör ändra detta så att det `kEventTimelineUpdated` bara lyssnar efter den. När enskilda annonsbrytningar har lösts skickas en ny `kEventTimelineUpdated` händelse.
