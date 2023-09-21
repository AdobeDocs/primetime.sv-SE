---
description: För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.
title: VOD-annonsmatchning och infogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# VOD-annonsmatchning och infogning{#vod-ad-resolving-and-insertion}

För VOD-innehåll (video-on-demand) infogar TVSDK annonsbrytningar genom att dela annonserna i huvudinnehållet så att tidslinjens varaktighet ökar.

Före uppspelning löser TVSDK kända annonser, infogar annonsbrytningar i huvudinnehållet enligt beskrivningen i en tidslinje som returneras från TVSDK och beräknar om den virtuella tidslinjen om det behövs.

TVSDK infogar annonser på följande sätt:

* **Före rullning**, som är före innehållet.
* **Mid-roll**, som finns i innehållet.
* **Efterrullning**, som kommer efter innehållet.

>[!IMPORTANT]
>
>Vid implementering av en anpassad `AdPolicySelector`kan olika principer ges för varje typ av `AdBreakTimelineItem` (förrullning, mittrullning eller efterrullning) in `AdPolicyInfo`, baserat på typen av `AdBreakTimelineItem`. Du kan t.ex. behålla innehåll i mitten av rullen efter att det har spelats upp, men ta bort innehåll före uppspelning.

När uppspelningen har startats kan inga ytterligare ändringar göras i innehållet. Ads cannot be:

* Infogad
* Borttagen

  Du kan t.ex. inte ta bort inbyggda annonser från innehållet för att erbjuda en reklamfri upplevelse.
* Ersatt

  Du kan till exempel inte ersätta inbyggda annonser med riktade annonser.
