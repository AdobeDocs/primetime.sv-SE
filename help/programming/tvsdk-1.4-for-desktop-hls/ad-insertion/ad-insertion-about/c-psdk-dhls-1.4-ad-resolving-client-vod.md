---
description: För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
seo-description: För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
seo-title: VOD-annonsmatchning och infogning
title: VOD-annonsmatchning och infogning
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# VOD-annonser som löser och infogar{#vod-ad-resolving-and-insertion}

För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.

Före uppspelning löser TVSDK kända annonser, infogar annonsbrytningar i huvudinnehållet enligt beskrivningen i en tidslinje som returneras från TVSDK och beräknar om den virtuella tidslinjen om det behövs.

TVSDK infogar annonser på följande sätt:

* **Pre-roll**, vilket är före innehållet.
* **Mid-roll**, som finns i innehållet.
* **Efterrullning**, som är efter innehållet.

>[!IMPORTANT]
>
>När du implementerar en anpassad `AdPolicySelector` kan olika profiler ges till varje typ av `AdBreakTimelineItem` (pre-roll, mid-roll eller post-roll) i `AdPolicyInfo`, baserat på typen för `AdBreakTimelineItem`. Du kan t.ex. behålla innehåll i mitten av rullen efter att det har spelats upp, men ta bort innehåll före uppspelning.

När uppspelningen har startats kan inga ytterligare ändringar göras i innehållet. Ads cannot be:

* Infogad
* Borttagen

   Du kan t.ex. inte ta bort inbyggda annonser från innehållet för att erbjuda en reklamfri upplevelse.
* Ersatt

   Du kan till exempel inte ersätta inbyggda annonser med riktade annonser.

