---
description: 'Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod '
title: 'Uppgradera från 2.5.x Lazy Ad Resolving till 3.0.0 Lazy Ad Resolving (API/Workflow changes) '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Uppgraderar från 2.5.x Lazy Ad Resolving to 3.x Lazy Ad Resolving (API/Workflow changes):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

Gränssnittet com.adobe.mediacore.timeline.TimelineMarker innehåller nu en ny metod:

**Placement.Type getPlacementType()**

Den här metoden returnerar placeringstypen Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL eller Placement.Type.POST_ROLL. Om en annonsbrytning inte löses returnerar metoden `getDuration()`i TimelineMarker-gränssnittet 0.

>[!NOTE]
>
>Det här gränssnittet typkonverteras inte alltid till typen com.mediacore.timeline.advertising.AdBreakTimelineItem om den ännu inte har lösts. Det kan kastas om metoden `getDuration()` för TimelineMarker är större än 0.

**Händelseändringar:**

`kEventAdResolutionComplete` är nu avskriven och aktiveras nu omedelbart efter att spelaren har förberetts. Program som tidigare bara lyssnade på den här händelsen för att rita rensningsfältet bör ändra detta så att det endast lyssnar efter `kEventTimelineUpdated`. När enskilda annonsbrytningar har lösts skickas en ny `kEventTimelineUpdated`-händelse.
